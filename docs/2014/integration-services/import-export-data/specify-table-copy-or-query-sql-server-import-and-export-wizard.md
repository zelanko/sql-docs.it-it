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
manager: craigg
ms.openlocfilehash: 524e878933652699bef6e31da42d3a784b54df7c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394419"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Impostazione copia tabella o query (Importazione/Esportazione guidata SQL Server)
  Usare la **impostazione copia tabella o Query** pagina per specificare la modalità copiare i dati. È possibile selezionare gli oggetti di database esistenti che si desidera copiare mediante l'interfaccia grafica oppure utilizzare Transact-SQL per creare una query più complessa.  
  
 Per altre informazioni su questa procedura guidata, vedere [SQL Server importazione / esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per altre informazioni sulle opzioni per avviare la procedura guidata, nonché le autorizzazioni necessarie per eseguire correttamente la procedura guidata, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Copia i dati da una o più tabelle o viste**  
 Copiare i campi da tabelle di origine selezionata e le viste per la destinazione specificata o le destinazioni usando il **selezionare le tabelle di origine e le viste** nella finestra di dialogo. Utilizzare questa opzione se si desidera copiare tutti i dati inclusi nell'origine senza filtrare o ordinare i record.  
  
 Quando si usa un' [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] provider di dati per la connessione all'origine dati, il **copiare i dati da uno o più tabelle o viste** opzione potrebbe non essere disponibili. Questa opzione è disponibile solo per i provider per cui è presente una sezione ProviderDescription nel file ProviderDescriptors.xml. Ogni sezione ProviderDescription contiene le informazioni necessarie per recuperare metadati dal provider corrispondente. Per impostazione predefinita, il file ProviderDescriptors.xml contiene una sezione ProviderDescription solo per i provider seguenti:  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 Per rendere il **copiare i dati da uno o più tabelle o viste** opzione disponibile per altri provider, terze parti possono aggiungere le proprie sezioni ProviderDescriptor al file Providerdescriptors. Per impostazione predefinita, questo file è nel \< *unità*>: \Programmi\Microsoft SQL Server\100\DTS\ProviderDescriptors. Per controllare i requisiti per la sezione ProviderDescriptor, vedere il file di schema ProviderDescriptors.xsd disponibile, per impostazione predefinita, nella stessa cartella del file ProviderDescriptors.xml.  
  
 **Scrivi una query per specificare i dati da trasferire**  
 Compilare le istruzioni SQL per recuperare righe utilizzando la **impostazione Query di origine** nella finestra di dialogo. Utilizzare questa opzione se si desidera modificare o limitare i dati di origine durante l'operazione di copia. È possibile copiare solo le righe che corrispondono ai criteri di selezione.  
  
  
