---
title: Finestra di dialogo Proprietà pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ff402435688d2471b7e6bd871a2e9a3f1cbd98c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68007994"
---
# <a name="package-properties-dialog-box"></a>Finestra di dialogo Proprietà pacchetto

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la finestra di dialogo **Proprietà pacchetto** per visualizzare le proprietà dei pacchetti archiviati nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Per altre informazioni, vedere [Server Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
 **Per saperne di più**  
  
-   [Aprire la finestra di dialogo Proprietà pacchetto](#open_dialog)  
  
-   [Configurare le opzioni](#options)  
  
##  <a name="open_dialog"></a> Aprire la finestra di dialogo Proprietà pacchetto  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il database SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Espandere la cartella che contiene il pacchetto di cui si desidera visualizzare le proprietà.  
  
5.  Fare clic con il pulsante destro del mouse sul pacchetto, quindi scegliere **Proprietà**.  
  
##  <a name="options"></a> Configurare le opzioni  
 Utilizzare la pagina **Generale** per visualizzare le proprietà del pacchetto selezionato.  
  
 Tutte le proprietà nella pagina **Generale** sono di sola lettura.  
  
 **Nome**  
 Viene visualizzato il nome del pacchetto.  
  
 **Identificatore**  
 Viene elencato l'ID del pacchetto.  
  
 **Punto di ingresso**  
 Con il valore **True** si indica che il pacchetto viene avviato direttamente. Con il valore **False** si indica che il pacchetto viene avviato da un altro pacchetto tramite l'attività Esegui pacchetto. Il valore predefinito è **True**.  
  
 Questa proprietà si imposta in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] sia per il pacchetto padre che per i pacchetti figlio facendo clic con il pulsante destro del mouse sul pacchetto in Esplora soluzioni e selezionando **Pacchetto punto di ingresso**.  
  
 **Descrizione**  
 Viene visualizzata la descrizione facoltativa del pacchetto.  
  
  
