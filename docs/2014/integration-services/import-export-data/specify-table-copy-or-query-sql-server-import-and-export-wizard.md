---
title: Impostazione copia tabella o query (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 51f195a9f5fbe97eadfc281ad50bd0de55d6151e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965531"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Impostazione copia tabella o query (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **impostazione Copia tabella o query** per specificare la modalità di copia dei dati. È possibile selezionare gli oggetti di database esistenti che si desidera copiare mediante l'interfaccia grafica oppure utilizzare Transact-SQL per creare una query più complessa.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni di avvio della procedura guidata, nonché sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Copiare dati da una o più tabelle o viste**  
 Consente di copiare i campi dalle tabelle e dalle viste di origine selezionate nella destinazione o nelle destinazioni specificate utilizzando la finestra di dialogo **Seleziona tabelle e viste di origine** . Utilizzare questa opzione se si desidera copiare tutti i dati inclusi nell'origine senza filtrare o ordinare i record.  
  
 Quando si utilizza un [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] provider di dati per connettersi all'origine dati, l'opzione **copia i dati da una o più tabelle o viste** potrebbe non essere disponibile. Questa opzione è disponibile solo per i provider per cui è presente una sezione ProviderDescription nel file ProviderDescriptors.xml. Ogni sezione ProviderDescription contiene le informazioni necessarie per recuperare metadati dal provider corrispondente. Per impostazione predefinita, il file ProviderDescriptors.xml contiene una sezione ProviderDescription solo per i provider seguenti:  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 Per rendere disponibili la **copia dei dati da una o più tabelle o viste** per provider aggiuntivi, terze parti possono aggiungere le proprie sezioni ProviderDescriptor al file ProviderDescriptors.xml. Per impostazione predefinita, il file si trova in \<*drive*> : \Programmi\Microsoft SQL Server\100\DTS\ProviderDescriptors. Per controllare i requisiti per la sezione ProviderDescriptor, vedere il file di schema ProviderDescriptors.xsd disponibile, per impostazione predefinita, nella stessa cartella del file ProviderDescriptors.xml.  
  
 **Scrivi una query per specificare i dati da trasferire**  
 Compilare istruzioni SQL per recuperare le righe utilizzando la finestra di dialogo **specificare una query di origine** . Utilizzare questa opzione se si desidera modificare o limitare i dati di origine durante l'operazione di copia. È possibile copiare solo le righe che corrispondono ai criteri di selezione.  
  
  
