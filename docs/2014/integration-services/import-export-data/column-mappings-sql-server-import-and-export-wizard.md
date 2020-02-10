---
title: Mapping colonne (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0108004bc7fb5743ab92c455f4aee99a9f3df498
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62893042"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Mapping colonne (Importazione/Esportazione guidata SQL Server)
  Utilizzare la finestra di dialogo **Mapping colonne** per modificare i parametri di trasformazione.  
  
> [!NOTE]  
>  Non è necessario copiare tutte le colonne in una tabella quando si seleziona l'opzione Copia tabella. Selezionare ** \<ignora>** nella colonna **destinazione** della finestra di dialogo per le colonne che si desidera ignorare.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni di avvio della procedura guidata, nonché sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
 **Origine**  
 Identifica la tabella, la visualizzazione o la query di origine selezionata.  
  
 **Destinazione**  
 Identifica la tabella, la visualizzazione o la query di destinazione selezionata.  
  
 **Crea tabella di destinazione/file**  
 Consente di specificare se creare la tabella di destinazione qualora non esista già.  
  
 **Elimina righe nella tabella di destinazione/file**  
 Consente di specificare se cancellare i dati da una tabella esistente prima di caricare nuovi dati.  
  
 **Accoda righe alla tabella/file di destinazione**  
 Consente di specificare se aggiungere nuovi dati a quelli già presenti in una tabella esistente.  
  
 **Modifica SQL**  
 Utilizzare l'istruzione predefinita nella finestra di dialogo **istruzione SQL CREATE TABLE** o modificarla per i propri scopi. Se si modifica questa istruzione, è necessario inoltre eseguire modifiche collegate al mapping della tabella.  
  
 **Elimina e ricrea tabella di destinazione**  
 Selezionare questa opzione per sovrascrivere la tabella di destinazione. Questa opzione è disponibile solo quando si utilizza la procedura guidata per creare la tabella di destinazione. La tabella di destinazione viene eliminata e ricreata solo se si salva il pacchetto creato dalla procedura guidata e quindi lo si esegue nuovamente.  
  
 **Abilita inserimento identità**  
 Selezionare questa opzione per consentire l'inserimento dei valori di identità esistenti nei dati di origine all'interno di una colonna Identity della tabella di destinazione. Per impostazione predefinita, non è possibile applicare questa opzione alla colonna Identity di destinazione.  
  
 **Mapping**  
 Consente di visualizzare la modalità di mapping tra ogni colonna nell'origine dati e una colonna nella destinazione.  
  
 L'elenco contiene le colonne seguenti:  
  
 **Origine**  
 Consente di visualizzare ogni colonna di origine da cui è possibile impostare parametri di trasformazione.  
  
 **Destinazione**  
 Consente di specificare se ignorare una colonna durante l'operazione di copia. È possibile copiare solo un subset di colonne selezionando ** \<ignora>** in questa colonna per le colonne che si desidera ignorare. Prima di eseguire il mapping delle colonne, è necessario ignorare tutte le colonne di cui non verrà eseguito il mapping.  
  
 **Tipo**  
 Consente di selezionare un tipo di dati per la colonna.  
  
 **Nullable**  
 Consente di specificare se una colonna può supportare un valore Null.  
  
 **Dimensione**  
 Consente di specificare il numero di caratteri nella colonna.  
  
 **Precision**  
 Consente di specificare la precisione dei dati visualizzati, indicando il numero di cifre.  
  
 **Scalabilità**  
 Consente di specificare la scala dei dati visualizzati, indicando il numero di posizioni decimali.  
  
  
