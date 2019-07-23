---
title: Selezione tabella dimensione e chiavi (Configurazione guidata dimensioni a modifica lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1d9a9ba09bfcf3f5fb3d8b1f1b751ac58d01a34f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928188"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Selezione tabella dimensione e chiavi (Configurazione guidata dimensioni a modifica lenta)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la pagina **Selezione tabella dimensione e chiavi** per selezionare una tabella della dimensione da caricare ed eseguire il mapping tra le colonne del flusso di dati e le colonne che verranno caricate.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Connection manager**  
 Selezionare una gestione connessione OLE DB esistente nell'elenco oppure fare clic su **Nuova** per creare una nuova gestione connessione OLE DB.  
  
> [!NOTE]  
>  La Configurazione guidata dimensioni a modifica lenta supporta solo le gestioni connessioni OLE DB e le connessioni a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nuova**  
 Nella finestra di dialogo **Configura gestione connessione OLE DB** selezionare una gestione connessione esistente oppure scegliere **Nuova** per creare una nuova connessione OLE DB.  
  
 **Tabella o vista**  
 Consente di selezionare una tabella o una vista dall'elenco.  
  
 **Colonne di input**  
 Consente di seleziona dall'apposito elenco le colonne di input per le quali è possibile definire il mapping.  
  
 **Colonne dimensione**  
 Consente di visualizzare tutte le colonne della dimensione disponibili.  
  
 **Tipo chiave**  
 Consente di selezionare una delle colonne della dimensione da utilizzare come chiave business. È necessario disporre di una chiave business.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione degli output tramite Configurazione guidata dimensioni a modifica lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
