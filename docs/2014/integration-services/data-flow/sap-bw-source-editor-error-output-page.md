---
title: Editor origine SAP BW (pagina Output degli errori) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6e23b0c-949a-46d1-8424-4dc3d9035e79
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8eb25ae1083e05ccb85dda6d07d391ca58d7951a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62770701"
---
# <a name="sap-bw-source-editor-error-output-page"></a>Editor origine SAP BW (pagina Output degli errori)
  Utilizzare la pagina **Output degli errori** della finestra di dialogo **Editor origine SAP BW** per selezionare le opzioni di gestione degli errori e impostare le proprietà delle colonne di output degli errori.  
  
 Per altre informazioni sul componente di origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 **Per aprire la pagina Output errori**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Output degli errori** per aprire la pagina **Output degli errori** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare l'origine, può essere necessario consultare l'amministratore SAP.  
  
 **Input o output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Visualizzare le colonne esterne (di origine) selezionate nella pagina **Colonne** della finestra di dialogo **Editor origine SAP BW** . Per altre informazioni su questa finestra di dialogo, vedere [Editor origine SAP BW &#40;pagina Colonne&#41;](sap-bw-source-editor-columns-page.md).  
  
 **Error (Errore) (Error (Errore)e)**  
 Specificare quale operazione dovrà essere eseguita dal componente di origine SAP BW in caso di errore: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Troncamento**  
 Specificare quale operazione dovrà essere eseguita dal componente di origine SAP BW in caso di troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione dell'errore.  
  
 **Imposta questo valore nelle celle selezionate**  
 Specificare l'azione che dovrà essere eseguita dal componente di origine SAP BW su tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor origine SAP BW &#40;pagina Colonne&#41;](sap-bw-source-editor-columns-page.md)   
 [Editor origine SAP BW &#40;pagina Avanzate&#41;](sap-bw-source-editor-advanced-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
