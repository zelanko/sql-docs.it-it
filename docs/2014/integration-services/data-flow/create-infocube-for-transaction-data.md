---
title: Crea InfoCube per dati transazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 673cea01-a260-4fce-a1a0-f73839289805
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6dbd26125679c95f20bbeea08fcffbc596b4e990
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432318"
---
# <a name="create-infocube-for-transaction-data"></a>Crea InfoCube per dati transazione
  Usare la finestra di dialogo **Crea InfoCube per dati transazione** per creare un nuovo InfoCube per i dati della transazione nel sistema SAP Netweaver BW.  
  
 È possibile aprire la finestra di dialogo **Crea InfoCube per dati transazione** dalla pagina **Gestione connessione** dell' **Editor destinazione SAP BW**. Per ulteriori informazioni sulla destinazione SAP BW, vedere [SAP BW Destination](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Crea InfoCube per dati transazione.**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella casella di gruppo **Crea oggetti SAP BW** della pagina **Gestione connessione** selezionare **InfoCube**, quindi fare clic su **Crea**.  
  
## <a name="general-options"></a>Opzioni generali  
 **Nome InfoCube**  
 Immettere un nome per il nuovo InfoCube.  
  
 **Descrizione lunga**  
 Immettere una descrizione per il nuovo InfoCube.  
  
 **Salva e attiva**  
 Salvare e attivare il nuovo InfoCube.  
  
## <a name="infocube-transfer-structure-options"></a>Opzioni della struttura di trasferimento di InfoCube  
 La sezione della struttura di trasferimento di InfoCube consente di associare le colonne del flusso di dati agli InfoObject.  
  
 **PipelineElement**  
 Visualizza la colonna nell'output del flusso di dati connesso alla destinazione SAP BW.  
  
 **PipelineDataType**  
 Visualizza il tipo di dati della colonna del flusso di dati.  
  
 **InfoObject**  
 Visualizza il nome dell'InfoObject associato alla colonna del flusso di dati.  
  
 **Tipo**  
 Visualizza il tipo dell'InfoObject associato alla colonna del flusso di dati. Nella tabella seguente sono elencati i valori possibili per il tipo.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|CHA|Caratteristiche|  
|UNI|Unità|  
|KYF|Cifre chiave|  
|TIM|Caratteristiche ora|  
  
 **Iobject - Ricerca**  
 Associare un InfoObject esistente alla colonna del flusso di dati per la riga corrente. Per effettuare questa associazione, fare clic su **Cerca**e quindi usare la finestra di dialogo **Cerca InfoObject** per selezionare l'InfoObject esistente. Per altre informazioni su questa finestra di dialogo, vedere [Cerca InfoObject](look-up-infoobject.md).  
  
 Dopo aver selezionato un InfoObject esistente, le colonne **InfoObject** e **Tipo** vengono popolate dal componente con i valori selezionati.  
  
 **Iobject - Nuovo**  
 Creare un nuovo InfoObject e associarlo alla colonna del flusso di dati nella riga corrente. Per creare il nuovo InfoObject, fare clic su **Nuovo**quindi usare la finestra di dialogo **Crea nuovo InfoObject** per creare l'InfoObject. Per altre informazioni su questa finestra di dialogo, vedere [Crea nuovo InfoObject](create-new-infoobject.md).  
  
 Dopo aver creato un nuovo InfoObject, le colonne **InfoObject** e **Tipo** vengono popolate dal componente con i nuovi valori.  
  
 **Iobject - Rimuovi**  
 Rimuovere l'associazione tra l'InfoObject e la colonna del flusso di dati per la riga corrente. Per rimuovere l'associazione, scegliere **Rimuovi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
