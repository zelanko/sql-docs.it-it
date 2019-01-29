---
title: I provider dell'archivio chiavi personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: 59a1458c98fb12f2f053bfd71649f40ddc5d1e4e
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55047215"
---
# <a name="custom-keystore-providers"></a>Provider di archivi chiavi personalizzati
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Panoramica

La funzionalità di crittografia di colonna di SQL Server 2016 richiede che il crittografati chiavi di crittografia colonna (ECEKs) archiviati nel server di essere recuperata dal client e quindi decrittografate alle chiavi di crittografia di colonna (Cek) per accedere ai dati archiviati nelle colonne crittografate. ECEKs vengono crittografate da chiavi Master della colonna (CMK), e la sicurezza di CMK è importante per la sicurezza della crittografia della colonna. Di conseguenza, le chiavi master di colonna devono essere archiviati in una posizione sicura; lo scopo di un Provider dell'archivio chiavi di crittografia delle colonne è fornire un'interfaccia per consentire il driver ODBC accedere in modo sicuro alle archiviati CMK. Per gli utenti con i propri archiviazione protetta, l'interfaccia del Provider dell'archivio chiavi personalizzato fornisce un framework per l'implementazione di accesso per la memorizzazione di CMK per il driver ODBC, che quindi può essere utilizzata per eseguire CEK crittografia e decrittografia protetta.

Ogni provider dell'archivio chiavi contiene e gestisce uno o più CMK, che sono identificati dai percorsi delle chiavi - le stringhe di un formato definito dal provider. Questa operazione, con l'algoritmo di crittografia, anche una stringa definita dal provider, utilizzabile per eseguire la crittografia di una CEK e la decrittografia di una chiave ECEK. L'algoritmo, con la chiave ECEK e il nome del provider, vengono archiviate nei metadati di crittografia del database. visualizzare [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) e [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) per altre informazioni. Di conseguenza, le due operazioni fondamentali della gestione delle chiavi sono:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

in cui il `CEKeystoreProvider_name` viene usato per identificare il Provider di archivio chiavi di crittografia (CEKeystoreProvider), colonna specifico e gli altri argomenti vengono utilizzati dal CEKeystoreProvider per crittografare/decrittografare la chiave CEK (E). Il nome e percorso chiave vengono forniti dai metadati di chiavi master di colonna, mentre l'algoritmo e il valore della chiave ECEK vengono forniti dai metadati della chiave CEK. Più provider di archivio chiavi possono essere presenti insieme i provider predefiniti predefinito. Durante un'operazione che richiede la CEK, il driver utilizza i metadati CMK per trovare il provider dell'archivio chiavi appropriata in base al nome ed esegue l'operazione di decrittografia, che può essere espresso come:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Anche se il driver non è necessario specificare per crittografare cek in più, uno strumento di gestione delle chiavi potrebbe essere necessario eseguire questa operazione per implementare operazioni quali la creazione di chiavi master di colonna e rotazione; Questa operazione richiede l'operazione inversa:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Interfaccia CEKeyStoreProvider

Questo documento descrive in dettaglio l'interfaccia CEKeyStoreProvider. Un provider dell'archivio chiavi che implementa questa interfaccia è utilizzabile da Microsoft ODBC Driver for SQL Server. Gli implementatori CEKeyStoreProvider è possono usare questa guida per lo sviluppo di provider di archivio chiavi personalizzato utilizzabile dal driver.

Una libreria del provider dell'archivio chiavi ("libreria del provider") è una libreria a collegamento dinamico che può essere caricata dal driver ODBC e contiene uno o più provider di archivio chiavi. Il simbolo `CEKeystoreProvider` devono essere esportate mediante una libreria del provider e l'indirizzo di una matrice con terminazione null di puntatori a `CEKeystoreProvider` strutture, uno per ogni provider dell'archivio chiavi all'interno della libreria.

Oggetto `CEKeystoreProvider` struttura definisce i punti di ingresso di un provider dell'archivio chiavi singolo:

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|Nome campo|Descrizione|
|:--|:--|
|`Name`|Il nome del provider dell'archivio chiavi. Non deve essere lo stesso come qualsiasi altro provider di archivio chiavi caricato in precedenza tramite il driver o presenti in questa libreria. Con terminazione null, wide-stringa di caratteri *.|
|`Init`|Funzione di inizializzazione. Se una funzione di inizializzazione non è obbligatorio, questo campo può essere null.|
|`Read`|Provider read (funzione). Può essere null se non è necessario.|
|`Write`|Funzione di scrittura provider. Obbligatorio se in lettura non è null. Può essere null se non è necessario.|
|`DecryptCEK`|Funzione di decrittografia chiave ECEK. Questa funzione è il motivo per l'esistenza di un provider dell'archivio chiavi e non può essere null.|
|`EncryptCEK`|Funzione di crittografia chiave CEK. Il driver non chiama questa funzione, ma viene fornito per consentire l'accesso a livello di codice per la Creazione chiave ECEK dagli strumenti di gestione delle chiavi. Può essere null se non è necessario.|
|`Free`|Funzione di terminazione. Può essere null se non è necessario.|

Fatta eccezione per gratuito, le funzioni in questa interfaccia tutti dispongono di una coppia di parametri, **ctx** e **onError**. Il primo identifica il contesto in cui la funzione viene chiamata, mentre quest'ultimo viene usato per la segnalazione degli errori. Visualizzare [contesti](#context-association) e [Error Handling](#error-handling) sotto per altre informazioni.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Nome segnaposto per una funzione di inizializzazione definito dal provider. Il driver chiama una volta, questa funzione dopo che un provider è stato caricato, ma prima della prima volta che è necessario eseguire la decrittografia di chiave ECEK o Read()/Write() richieste. Utilizzare questa funzione per eseguire le operazioni di inizializzazione che necessari. 

|Argomento|Descrizione|
|:--|:--|
|`ctx`|[Input] Contesto dell'operazione.|
|`onError`|[Input] Funzione di segnalazione degli errori.|
|`Return Value`|Restituito diverso da zero per indicare l'esito positivo o zero per indicare l'esito negativo.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Nome segnaposto per una funzione di comunicazione definito dal provider. Il driver chiama questa funzione quando l'applicazione richiede per leggere i dati da un (precedentemente scritto-in) provider usando l'attributo di connessione SQL_COPT_SS_CEKEYSTOREDATA, consentendo all'applicazione di leggere i dati arbitrari dal provider. Visualizzare [comunica con i provider dell'archivio chiavi](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) per altre informazioni.

|Argomento|Descrizione|
|:--|:--|
|`ctx`|[Input] Contesto dell'operazione.|
|`onError`|[Input] Funzione di segnalazione degli errori.|
|`data`|[Output] Puntatore a un buffer in cui il provider scrive i dati da leggere dall'applicazione. Corrisponde al campo dati della struttura CEKEYSTOREDATA.|
|`len`|[InOut] Puntatore a un valore di lunghezza. al momento di input, questa è la lunghezza massima del buffer di dati e il provider non deve scrivere più * len byte a esso. Al termine, è necessario aggiornare il provider * len con il numero di byte effettivamente scritti.|
|`Return Value`|Restituito diverso da zero per indicare l'esito positivo o zero per indicare l'esito negativo.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Nome segnaposto per una funzione di comunicazione definito dal provider. Il driver chiama questa funzione quando l'applicazione richiede di scrivere dati in un provider tramite l'attributo di connessione SQL_COPT_SS_CEKEYSTOREDATA, consentendo all'applicazione di scrivere i dati arbitrari nel provider. Visualizzare [comunica con i provider dell'archivio chiavi](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) per altre informazioni.

|Argomento|Descrizione|
|:--|:--|
|`ctx`|[Input] Contesto dell'operazione.|
|`onError`|[Input] Funzione di segnalazione degli errori.|
|`data`|[Input] Puntatore a un buffer contenente i dati per il provider per la lettura. Corrisponde al campo dati della struttura CEKEYSTOREDATA. Il provider non deve leggere più len byte da questo buffer.|
|`len`|[Input] Il numero di byte disponibili nei dati. Corrisponde al campo della struttura CEKEYSTOREDATA dataSize.|
|`Return Value`|Restituito diverso da zero per indicare l'esito positivo o zero per indicare l'esito negativo.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Nome segnaposto per una funzione di decrittografia chiave ECEK definito dal provider. Il driver chiama questa funzione per decrittografare una chiave ECEK crittografata da una chiave CMK associate al provider in una CEK.

|Argomento|Descrizione|
|:--|:--|
|`ctx`|[Input] Contesto dell'operazione.|
|`onError`|[Input] Funzione di segnalazione degli errori.|
|`keyPath`|[Input] Il valore della [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) attributo di metadati per la chiave CMK fa riferimento la chiave ECEK specificata. Con terminazione null wide-stringa di caratteri *. Ciò consente di identificare una CMK gestita da questo provider.|
|`alg`|[Input] Il valore della [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) attributo di metadati per la chiave ECEK specificata. Con terminazione null wide-stringa di caratteri *. Ciò consente di identificare l'algoritmo di crittografia usata per crittografare la chiave ECEK specificata.|
|`ecek`|[Input] Puntatore per la chiave ECEK da decrittografare.|
|`ecekLen`|[Input] Lunghezza della chiave ECEK.|
|`cekOut`|[Output] Il provider deve allocare memoria per la chiave ECEK decrittografata e scrivere il relativo indirizzo all'indicatore di misura a cui punta cekOut. Deve essere possibile liberare questo blocco di memoria usando il [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) o gratuito (funzione) (Linux/Mac). Se non è memoria allocata a causa di un errore o in caso contrario, il provider deve impostare * cekOut a un puntatore null.|
|`cekLen`|[Output] Il provider di scrivere all'indirizzo a cui punta cekLen la lunghezza della chiave ECEK decrittografata in cui è scritto per * * cekOut.|
|`Return Value`|Restituito diverso da zero per indicare l'esito positivo o zero per indicare l'esito negativo.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Nome segnaposto per una funzione di crittografia chiave CEK definito dal provider. Il driver non chiamare questa funzione e non esporre le proprie funzionalità tramite l'interfaccia ODBC, ma viene fornito per consentire l'accesso a livello di codice per la Creazione chiave ECEK dagli strumenti di gestione delle chiavi.

|Argomento|Descrizione|
|:--|:--|
|`ctx`|[Input] Contesto dell'operazione.|
|`onError`|[Input] Funzione di segnalazione degli errori.|
|`keyPath`|[Input] Il valore della [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) attributo di metadati per la chiave CMK fa riferimento la chiave ECEK specificata. Con terminazione null wide-stringa di caratteri *. Ciò consente di identificare una CMK gestita da questo provider.|
|`alg`|[Input] Il valore della [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) attributo di metadati per la chiave ECEK specificata. Con terminazione null wide-stringa di caratteri *. Ciò consente di identificare l'algoritmo di crittografia usata per crittografare la chiave ECEK specificata.|
|`cek`|[Input] Puntatore alla CEK deve essere crittografato.|
|`cekLen`|[Input] Lunghezza della chiave CEK.|
|`ecekOut`|[Output] Il provider deve allocare memoria per la CEK crittografata e scrivere il relativo indirizzo all'indicatore di misura a cui punta ecekOut. Deve essere possibile liberare questo blocco di memoria usando il [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) o gratuito (funzione) (Linux/Mac). Se non è memoria allocata a causa di un errore o in caso contrario, il provider deve impostare * ecekOut a un puntatore null.|
|`ecekLen`|[Output] Il provider di scrivere all'indirizzo a cui punta ecekLen la lunghezza della chiave CEK crittografata in cui è scritto per * * ecekOut.|
|`Return Value`|Restituito diverso da zero per indicare l'esito positivo o zero per indicare l'esito negativo.|

```
void (*Free)();
```
Nome segnaposto per una funzione di terminazione definito dal provider. Il driver può chiamare questa funzione al momento della terminazione normale del processo.

> [!NOTE]
> *Le stringhe di caratteri "wide" sono caratteri a 2 byte (UTF-16) a causa di un modo in cui SQL Server li archivia.*


### <a name="error-handling"></a>Gestione degli errori

Come possono verificarsi errori durante l'elaborazione di un provider di servizi, viene fornito un meccanismo per consentire la segnala gli errori al driver in modo dettagliato più specifica rispetto a un booleano esito positivo o negativo. Molte delle funzioni di disporre di una coppia di parametri **ctx** e **onError**, che vengono utilizzati insieme a questo scopo oltre il valore restituito esito positivo o negativo.

Il **ctx** parametro identifica il contesto in cui viene eseguita un'operazione di provider.

Il **onError** parametro punta a una funzione di segnalazione degli errori, con il prototipo seguente:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argomento|Descrizione|
|:--|:--|
|`ctx`|[Input] Il contesto per segnalare l'errore.|
|`msg`|[Input] Il messaggio di errore al report. Stringa con terminazione null di caratteri wide. Per consentire di informazioni con parametri sia presente, questa stringa può contenere le sequenze di formattazione di inserimento nel formato accettato dal [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) (funzione). La funzionalità estesa può essere specificata da questo parametro, come descritto di seguito.|
|...|[Input] Parametri variadic aggiuntive per gli identificatori di formato di messaggio, come appropriato.|

Per segnalare quando si è verificato un errore, la funzione provider onError le chiamate provider, fornendo il parametro di contesto passato dal driver e un messaggio di errore con parametri aggiuntivi facoltativi da formattare in esso. Il provider può chiamare questa funzione più volte per inviare più messaggi di errore consecutivamente all'interno di chiamata di una funzione del provider. Ad esempio

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


Il `msg` parametro consiste in genere una stringa di caratteri "wide", ma sono disponibili estensioni aggiuntive:

Utilizzando uno dei valori predefiniti speciali con la macro IDS_MSG, i messaggi di errore generico già esistenti e in un form localizzato nel driver possono essere utilizzate. Ad esempio, se un provider non riesce ad allocare memoria, il `IDS_S1_001` messaggio "Errore di allocazione della memoria" può essere utilizzato:

`onError(ctx, IDS_MSG(IDS_S1_001));`

Per l'errore essere riconosciuti dal driver, la funzione del provider deve restituire un errore. Quando questa operazione viene eseguita nel contesto di un'operazione di ODBC, gli errori registrati diventa accessibili nell'handle di connessione o l'istruzione tramite il meccanismo di diagnostica ODBC standard (`SQLError`, `SQLGetDiagRec`, e `SQLGetDiagField`).


### <a name="context-association"></a>Associazione di contesto

Il `CEKEYSTORECONTEXT` struttura, oltre a fornire il contesto per il callback di errore, nonché per determinare il contesto ODBC in cui viene eseguita un'operazione del provider. Ciò consente a un provider associare dati a ciascuno di questi contesti, ad esempio, per implementare la configurazione per ogni connessione. A tale scopo, la struttura contiene 3 puntatori opachi corrispondente al contesto dell'ambiente, connessione e istruzione:

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|Campo|Descrizione|
|:--|:--|
|`envCtx`|Contesto dell'ambiente.|
|`dbcCtx`|Contesto di connessione.|
|`stmtCtx`|Contesto di istruzioni.|

Ognuno di questi contesti è un valore opaco che, mentre non lo stesso handle ODBC per la corrispondente, è utilizzabile come identificatore univoco per l'handle: se gestiscono *X* viene associato il valore di contesto *Y*, quindi Nessun altri handle di ambiente, connessione o dell'istruzione che sono presenti contemporaneamente allo stesso tempo come *X* avrà un valore di contesto *Y*, e nessun altro valore di contesto verranno associato gestire *X*. Se l'operazione di provider eseguito non dispone di un contesto di un handle specifico (ad esempio, chiamate di SQLSetConnectAttr per caricare e configurare i provider, in cui non c'è alcun handle di istruzione) il corrispondente valore di contesto nella struttura è null.


## <a name="example"></a>Esempio

### <a name="keystore-provider"></a>Provider dell'archivio chiavi

Il codice riportato di seguito è riportato un esempio di un'implementazione del provider dell'archivio chiavi minime.

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>Applicazione ODBC

Il codice seguente è un'applicazione demo che utilizza il provider dell'archivio chiavi precedente. Se viene eseguito, assicurarsi che la libreria del provider nella stessa directory del file binario dell'applicazione, e che specifica la stringa di connessione (o specifica un DSN che contiene) il `ColumnEncryption=Enabled` impostazione.

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>Vedere anche

[Using Always Encrypted with the ODBC Driver](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) (Utilizzo di Always Encrypted con il driver ODBC)
