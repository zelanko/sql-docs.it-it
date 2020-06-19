---
title: Selezione tabella dimensione e chiavi (Configurazione guidata dimensioni a modifica lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6207f01290b21c556ed16a836d12974d227e2d3c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939342"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Selezione tabella dimensione e chiavi (Configurazione guidata dimensioni a modifica lenta)
  Utilizzare la pagina **Selezione tabella dimensione e chiavi** per selezionare una tabella della dimensione da caricare ed eseguire il mapping tra le colonne del flusso di dati e le colonne che verranno caricate.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Connection manager**  
 Selezionare una gestione connessione OLE DB esistente nell'elenco oppure fare clic su **Nuova** per creare una nuova gestione connessione OLE DB.  
  
> [!NOTE]  
>  La Configurazione guidata dimensioni a modifica lenta supporta solo le gestioni connessioni OLE DB e le connessioni a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nuovo**  
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
 [Configurare gli output tramite Configurazione guidata dimensioni a modifica lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
