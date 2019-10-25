---
title: Uso di Azure Active Directory | Microsoft Docs per SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: b459877be731da11b33d13772bbf186ecf72198c
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381847"
---
# <a name="using-azure-active-directory"></a>Uso di Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Scopo

A partire dalla versione 18.2.1, il driver Microsoft OLE DB per SQL Server consente alle applicazioni OLE DB di connettersi a un'istanza del database SQL di Azure usando un'identità federata. I nuovi metodi di autenticazione includono:
- ID di accesso e password Azure Active Directory
- Token di accesso di Azure Active Directory
- Autenticazione integrata di Azure Active Directory
- ID e password di accesso SQL

La versione 18,3 aggiunge il supporto per i metodi di autenticazione seguenti:
- Autenticazione interattiva di Azure Active Directory
- Autenticazione MSI di Azure Active Directory

> [!NOTE]
> L'utilizzo delle modalità di autenticazione seguenti con `DataTypeCompatibility` (o la proprietà corrispondente) impostata su `80` **non** è supportato:
> - Autenticazione Azure Active Directory tramite ID e password di accesso
> - Autenticazione Azure Active Directory usando il token di accesso
> - Autenticazione integrata di Azure Active Directory
> - Autenticazione interattiva di Azure Active Directory
> - Autenticazione MSI di Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>Parole chiave e proprietà della stringa di connessione
Per supportare l'autenticazione Azure Active Directory sono state introdotte le seguenti parole chiave della stringa di connessione:

|Parola chiave stringa di connessione|Proprietà di connessione|Descrizione|
|---               |---                |---        |
|Token di accesso|SSPROP_AUTH_ACCESS_TOKEN|Specifica un token di accesso per l'autenticazione Azure Active Directory. |
|Autenticazione|SSPROP_AUTH_MODE|Specifica il metodo di autenticazione da usare.|

Per ulteriori informazioni sulle nuove parole chiave/proprietà, vedere le pagine seguenti:
- [Utilizzo delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Proprietà di inizializzazione e di autorizzazione](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Crittografia e convalida di certificati
In questa sezione vengono descritte le modifiche apportate al comportamento di crittografia e convalida dei certificati. Queste modifiche sono effettive **solo** quando si usano le parole chiave della stringa di connessione del nuovo token di autenticazione o di accesso (o le proprietà corrispondenti).

### <a name="encryption"></a>Crittografia
Per migliorare la sicurezza, quando vengono utilizzate le nuove proprietà/parole chiave di connessione, il driver sostituisce il valore di crittografia predefinito impostandolo su `yes`. L'override si verifica al momento dell'inizializzazione dell'oggetto origine dati. Se la crittografia viene impostata prima dell'inizializzazione con qualsiasi mezzo, il valore viene rispettato e non viene sottoposto a override.

> [!NOTE]   
> Nelle applicazioni ADO e nelle applicazioni che ottengono l'interfaccia `IDBInitialize` tramite `IDataInitialize::GetDataSource`, il componente di base che implementa l'interfaccia imposta in modo esplicito la crittografia sul valore predefinito di `no`. Di conseguenza, le nuove proprietà/parole chiave di autenticazione rispettano questa impostazione e il valore di crittografia **non** viene sottoposto a override. Pertanto, è **consigliabile** impostare in modo esplicito `Use Encryption for Data=true` per eseguire l'override del valore predefinito.

### <a name="certificate-validation"></a>Convalida del certificato
Per migliorare la sicurezza, le nuove proprietà/parole chiave di connessione rispettano l'impostazione di `TrustServerCertificate` (e le parole chiave/proprietà della stringa di connessione corrispondenti) **indipendentemente dall'impostazione della crittografia client**. Di conseguenza, il certificato del server viene convalidato per impostazione predefinita.

> [!NOTE]   
> La convalida del certificato può anche essere controllata tramite il campo `Value` della voce del registro di sistema `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`. I valori validi sono `0` o `1`. Il driver OLE DB sceglie l'opzione più sicura tra il registro di sistema e le impostazioni di proprietà/parole chiave di connessione. Ovvero, il driver convaliderà il certificato server purché almeno una delle impostazioni del registro di sistema/connessione consenta la convalida del certificato del server.

## <a name="gui-additions"></a>Aggiunte GUI
L'interfaccia utente grafica del driver è stata migliorata per consentire l'autenticazione Azure Active Directory. Per altre informazioni, vedere:
- [Finestra di dialogo di accesso a SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configurazione di UDL (Universal Data Link)](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Esempi di stringhe di connessione
In questa sezione vengono illustrati esempi di parole chiave della stringa di connessione nuove ed esistenti da usare con `IDataInitialize::GetDataSource` e `DBPROP_INIT_PROVIDERSTRING` proprietà.

### <a name="sql-authentication"></a>Autenticazione SQL
- Utilizzo di `IDataInitialize::GetDataSource`:
    - Nuovo:
        > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = sqlpassword**; ID utente = [nomeutente]; Password = [password]; Usa crittografia per dati = true
    - Deprecato:
        > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; ID utente = [nomeutente]; Password = [password]; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    - Nuovo:
        > Server = [Server];D atabase = [database]; **Autenticazione = sqlpassword**; UID = [nomeutente]; PWD = [password]; Crittografia = Sì
    - Deprecato:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>Autenticazione integrata di Windows tramite SSPI (Security Support Provider Interface)

- Utilizzo di `IDataInitialize::GetDataSource`:
    - Nuovo:
        > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = ActiveDirectoryIntegrated**; Usa crittografia per dati = true
    - Deprecato:
        > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Sicurezza integrata = SSPI**; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    - Nuovo:
        > Server = [Server];D atabase = [database]; **Autenticazione = ActiveDirectoryIntegrated**; Crittografia = Sì
    - Deprecato:
        > Server = [Server];D atabase = [database]; **Trusted_Connection = Yes**; Crittografia = Sì

### <a name="azure-active-directory-username-and-password-authentication"></a>Autenticazione del nome utente e della password Azure Active Directory

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = ActiveDirectoryPassword**; ID utente = [nomeutente]; Password = [password]; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Autenticazione integrata di Azure Active Directory

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = ActiveDirectoryIntegrated**; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [Server];D atabase = [database]; **Autenticazione = ActiveDirectoryIntegrated**; Crittografia = Sì

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Azure Active Directory l'autenticazione tramite un token di accesso

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Token di accesso = [token di accesso]** ; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Fornire il token di accesso tramite `DBPROP_INIT_PROVIDERSTRING` non è supportato

### <a name="azure-active-directory-interactive-authentication"></a>Autenticazione interattiva di Azure Active Directory

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = ActiveDirectoryInteractive**; ID utente = [nomeutente]; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [Server];D atabase = [database]; **Autenticazione = ActiveDirectoryInteractive**; UID = [nomeutente]; Crittografia = Sì

### <a name="azure-active-directory-msi-authentication"></a>Autenticazione MSI di Azure Active Directory

- Utilizzo di `IDataInitialize::GetDataSource`:
    - Identità gestita assegnata dall'utente:
        > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = ActiveDirectoryMSI**; ID utente = [ID oggetto]; Usa crittografia per dati = true
    - Identità gestita assegnata dal sistema:
        > Provider = MSOLEDBSQL; origine dati = [Server]; catalogo iniziale = [database]; **Autenticazione = ActiveDirectoryMSI**; Usa crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    - Identità gestita assegnata dall'utente:
        > Server = [Server];D atabase = [database]; **Autenticazione = ActiveDirectoryMSI**; UID = [ID oggetto]; Crittografia = Sì
    - Identità gestita assegnata dal sistema:
        > Server = [Server];D atabase = [database]; **Autenticazione = ActiveDirectoryMSI**; Crittografia = Sì

## <a name="code-samples"></a>Esempi di codice

Negli esempi seguenti viene illustrato il codice necessario per connettersi a Azure Active Directory con le parole chiave di connessione. 

### <a name="access-token"></a>Token di accesso
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Integrato in Active Directory
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>Passaggi successivi
- [Autorizzare l'accesso alle applicazioni web Azure Active Directory usando il flusso di concessione del codice OAuth 2,0](https://go.microsoft.com/fwlink/?linkid=2072672).

- Informazioni sull'[autenticazione di Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2073783) in SQL Server.

- Configurare le connessioni driver usando le [parole chiave della stringa di connessione](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) supportate dal driver OLE DB.
