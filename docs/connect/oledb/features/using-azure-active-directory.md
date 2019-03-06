---
title: Uso di Azure Active Directory | Documentazione di Microsoft per SQL Server
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 44f92e782a497005ea47847301279e4341722d36
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744823"
---
# <a name="using-azure-active-directory"></a>Uso di Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Scopo

A partire dalla versione 18.2.1, il Driver Microsoft OLE DB per SQL Server consente applicazioni OLE DB per connettersi a un'istanza di Database SQL di Azure usando un'identità federata. I nuovi metodi di autenticazione includono:
- ID account di accesso di Azure Active Directory e la password
- Token di accesso di Azure Active Directory
- Autenticazione integrata di Azure Active Directory
- ID di accesso e password

> [!NOTE]  
> Quando si usa le seguenti opzioni di Azure Active Directory con il driver OLE DB, assicurarsi che il [Active Directory Authentication Library per SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) è stata installata:
> - ID account di accesso di Azure Active Directory e la password
> - Autenticazione integrata di Azure Active Directory
>
> ADAL non è necessaria per altri metodi di autenticazione o operazioni di OLE DB.

> [!NOTE]
> Usando le seguenti modalità di autenticazione con `DataTypeCompatibility` (o la proprietà corrispondente) impostata su `80` viene **non** supportati:
> - Autenticazione di Azure Active Directory con l'ID di accesso e password
> - Autenticazione di Azure Active Directory usando token di accesso
> - Autenticazione integrata di Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>Le proprietà e parole chiave delle stringhe di connessione
Parole chiave delle stringhe di connessione seguenti sono state introdotte per supportare l'autenticazione di Azure Active Directory:

|Parola chiave stringa di connessione|Proprietà di connessione|Descrizione|
|---               |---                |---        |
|Token di accesso|SSPROP_AUTH_ACCESS_TOKEN|Specifica un token di accesso per l'autenticazione ad Azure Active Directory. |
|Autenticazione|SSPROP_AUTH_MODE|Specifica il metodo di autenticazione da usare.|

Per altre informazioni sulle nuove parole chiave o proprietà, vedere le pagine seguenti:
- [Utilizzo delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Proprietà di inizializzazione e di autorizzazione](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Crittografia e convalida dei certificati
In questa sezione vengono illustrate le modifiche nel comportamento di convalida di certificati e crittografia. Queste modifiche saranno **solo** quando si usa il nuovo Token di accesso o l'autenticazione connessione parole chiave della stringa (o le proprietà corrispondenti) in vigore.

### <a name="encryption"></a>Crittografia
Per migliorare la sicurezza, quando si utilizzano le nuove proprietà di connessione/parole chiave, il driver sostituisce il valore di crittografia predefinito impostandolo su `yes`. Si esegue l'override si verifica in fase di inizializzazione di oggetti origine dati. Se la crittografia viene impostata prima dell'inizializzazione con qualsiasi mezzo, il valore viene rispettato e non viene sottoposto a override.

> [!NOTE]   
> Nelle applicazioni ADO e nelle applicazioni che ottengono la `IDBInitialize` interfacciarsi tramite `IDataInitialize::GetDataSource`, il componente di base che implementa l'interfaccia in modo esplicito imposta la crittografia per il valore predefinito di `no`. Di conseguenza, le nuove proprietà di autenticazione/parole chiave rispettano questa impostazione e il valore di crittografia **non è** sottoposto a override. È pertanto **consigliato** queste applicazioni viene impostata in modo esplicito `Use Encryption for Data=true` per sostituire il valore predefinito.

### <a name="certificate-validation"></a>Convalida del certificato
Per migliorare la sicurezza, le nuove proprietà di connessione/parole chiave rispetta il `TrustServerCertificate` impostazione (e le corrispondenti proprietà stringa di connessione parole chiave /) **indipendentemente dall'impostazione della crittografia client**. Di conseguenza, per impostazione predefinita è convalidare certificato del server.

> [!NOTE]   
> Convalida del certificato può essere controllata anche tramite il `Value` campo il `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` voce del Registro di sistema. I valori validi sono `0` o `1`. Il driver OLE DB sceglie l'opzione più sicura tra il Registro di sistema e le impostazioni o parola chiave della proprietà di connessione. Vale a dire, il driver convaliderà il certificato del server, purché almeno una delle impostazioni del Registro di sistema/connessione abilita la convalida del certificato server.

## <a name="gui-additions"></a>Aggiunte di interfaccia utente grafica
L'interfaccia utente grafica di driver è stato migliorato per consentire l'autenticazione di Azure Active Directory. Per altre informazioni, vedere:
- [Finestra di dialogo di accesso a SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configurazione di Universal Data Link (UDL)](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Esempi di stringhe di connessione
In questa sezione vengono illustrati esempi di connessione nuova ed esistente parole chiave della stringa da usare con `IDataInitialize::GetDataSource` e `DBPROP_INIT_PROVIDERSTRING` proprietà.

### <a name="sql-authentication"></a>Autenticazione SQL
- Utilizzo di `IDataInitialize::GetDataSource`:
    - Nuovo:
        > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; **Authentication = SqlPassword**; ID utente = [username]; Password = [password]; Utilizzare la crittografia per dati = true
    - Deprecato:
        > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; ID utente = [username]; Password = [password]; Utilizzare la crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    - Nuovo:
        > Server = [server], Database = [database]; **Authentication = SqlPassword**; UID = [username]; PWD = [password]; Crittografare = Sì
    - Deprecato:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>Autenticazione integrata di Windows tramite Security Support Provider Interface (SSPI)

- Utilizzo di `IDataInitialize::GetDataSource`:
    - Nuovo:
        > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; **Authentication = ActiveDirectoryIntegrated**; Utilizzare la crittografia per dati = true
    - Deprecato:
        > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; **La sicurezza integrata = SSPI**; Utilizzare la crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    - Nuovo:
        > Server = [server], Database = [database]; **Authentication = ActiveDirectoryIntegrated**; Crittografare = Sì
    - Deprecato:
        > Server = [server], Database = [database]; **Trusted_Connection = yes**; Crittografare = Sì

### <a name="aad-username-and-password-authentication-using-adal"></a>Autenticazione di nome utente e password AAD usando ADAL

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; **Authentication = ActiveDirectoryPassword**; ID utente = [username]; Password = [password]; Utilizzare la crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>Autenticazione integrata di Azure Active Directory usando ADAL

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; **Authentication = ActiveDirectoryIntegrated**; Utilizzare la crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [server], Database = [database]; **Authentication = ActiveDirectoryIntegrated**; Crittografare = Sì

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Autenticazione di Azure Active Directory usando un token di accesso

- Utilizzo di `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; origine dati = [server]; Initial Catalog = [database]; **Token di accesso = [token di accesso]**; Utilizzare la crittografia per dati = true
- Utilizzo di `DBPROP_INIT_PROVIDERSTRING`:
    > Che fornisce token di accesso tramite `DBPROP_INIT_PROVIDERSTRING` non è supportato

## <a name="code-samples"></a>Esempi di codice

Gli esempi seguenti illustrano il codice necessario per connettersi ad Azure Active Directory con parole chiave della connessione. 

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
- [Autorizzare l'accesso alle applicazioni web di Azure Active Directory tramite il flusso di concessione del codice OAuth 2.0](https://go.microsoft.com/fwlink/?linkid=2072672).

- Informazioni sull'[autenticazione di Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2073783) in SQL Server.

- Configurare connessioni driver usando [parole chiave delle stringhe di connessione](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) il driver supporta OLE DB.
