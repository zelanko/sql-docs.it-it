---
description: Visualizzazione o modifica di word breaker e filtri registrati
title: Visualizzare o modificare filtri registrati e word breaker
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], word breakers
- full-text search [SQL Server], filters
- filters [full-text search]
- word breakers [full-text search]
ms.assetid: f88c54df-b1aa-4701-807f-dc92c32363fd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: ec6bffa39e5f7a9b3bb1938f42dac110b8385da5
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868931"
---
# <a name="view-or-change-registered-filters-and-word-breakers"></a>Visualizzazione o modifica di word breaker e filtri registrati
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Dopo l'installazione o la disinstallazione di word breaker o filtri in un sistema, le modifiche non diventano automaticamente effettive nelle istanze server. In questo argomento viene descritto come visualizzare i word breaker o i filtri registrati, nonché come registrare i word breaker e i filtri appena installati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="to-view-a-list-of-languages-whose-word-breakers-are-currently-registered"></a>Per visualizzare un elenco delle lingue i cui word breaker sono registrati  
  
1.  Usare la vista del catalogo [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) , come illustrato di seguito:  
  
    ```  
    SELECT * FROM sys.fulltext_languages;   
    ```  
  
### <a name="to-view-a-list-of-the-filters-that-are-currently-registered"></a>Per visualizzare un elenco dei filtri registrati  
  
1.  Usare [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , come illustrato di seguito:  
  
    ```  
    EXEC sp_help_fulltext_system_components 'filter';    
    ```  
  
### <a name="to-register-newly-installed-word-breakers-and-filters"></a>Per registrare i word breaker e i filtri appena installati  
  
1.  Usare la stored procedure di sistema [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md) per aggiornare l'elenco di lingue, come illustrato di seguito:  
  
    ```  
    exec sp_fulltext_service 'update_languages';   
    ```  
  
### <a name="to-unregister-uninstalled-word-breakers-and-filters"></a>Per annullare la registrazione di word breaker e filtri disinstallati  
  
1.  Usare **sp_fulltext_service** per aggiornare l'elenco di lingue nel modo seguente:  
  
    ```  
    exec sp_fulltext_service 'update_languages'  
    ```  
  
2.  Usare **sp_fulltext_service** per riavviare i processi host del daemon di filtri (fdhost.exe) nel modo seguente:  
  
    ```  
    exec sp_fulltext_service 'restart_all_fdhosts';  
    ```  
  
### <a name="to-replace-existing-word-breakers-or-filters-when-installing-new-ones"></a>Per sostituire i word breaker o i filtri esistenti dopo averne installati di nuovi  
  
1.  Quando si prepara l'installazione di un file DLL contenente nuovi word breaker o filtri, verificare che il nome sia diverso da quelli di eventuali file DLL installati nell'istanza del server.  
  
2.  Copiare il nuovo file DLL nella directory contenente i file DLL standard di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'istanza server. Il percorso predefinito è:  
  
     C:\Programmi\Microsoft SQL Server\MSSQL.*nome_istanza*\MSSQL\Binn  
  
    > [!IMPORTANT]  
    >  Si consiglia di caricare solo componenti firmati e verificati. È inoltre consigliabile eseguire il servizio dell'utilità di avvio FDHOST (MSSQLFDLauncher) con privilegi minimi.  
  
3.  Installare i nuovi word breaker o filtri.  
  
     **Per installare e caricare filtri IFilter di Microsoft Filter Pack**  
  
    -   [Come registrare IFilter di Microsoft Filter Pack con SQL Server]()  
  
4.  Usare **sp_fulltext_service** per caricare i word breaker e i filtri appena installati nell'istanza del server nel modo seguente:  
  
    ```  
    EXEC sp_fulltext_service @action='load_os_resources', @value=1;  
    ```  
  
5.  Usare **sp_fulltext_service** per aggiornare l'elenco di lingue nel modo seguente:  
  
    ```  
    EXEC sp_fulltext_service 'update_languages';  
    ```  
  
6.  Riavviare i processi host del daemon di filtri (fdhost.exe) usando **sp_fulltext_service** nel modo seguente:  
  
    ```  
    EXEC sp_fulltext_service 'restart_all_fdhosts';   
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazione dell'account del servizio dell'Utilità di avvio del daemon di filtri full-text](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Configurazione e gestione di filtri per la ricerca](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Configurazione e gestione di word breaker e stemmer per la ricerca](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
