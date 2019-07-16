---
title: Importare i Management Pack di SCOM - sistema di piattaforma Analitica | Microsoft Docs
description: Seguire questi passaggi per importare i Management Pack di System Center Operations Manager (SCOM) per Analitica piattaforma di strumenti analitici. I management pack sono necessari per monitorare Parallel Data Warehouse da SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 070e7b73614f6884e45a5c91603d6086613d15ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960852"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importare il Management Pack SCOM - sistema di piattaforma Analitica
Seguire questi passaggi per importare i Management Pack di System Center Operations Manager (SCOM) per Analitica piattaforma di strumenti analitici. I management pack sono necessari per monitorare Parallel Data Warehouse da SCOM. 
  
## <a name="BeforeBegin"></a>Prima di iniziare  
**Prerequisiti**  
  
System Center Operations Manager 2007 R2 deve essere installato e in esecuzione.  
  
I management pack deve essere installato. Visualizzare [installa i Management Pack SCOM &#40;sistema di piattaforma Analitica&#41;](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Passaggio 1: Importare il Base Management Pack SQL Server Appliance  
  
1.  Accedere al computer con un account membro del ruolo amministratori di Operations Manager per il gruppo di gestione di Operations Manager 2007.  
  
2.  Nella console operatore, fare clic su **amministrazione**.  
  
3.  Fare doppio clic il **Management Pack** nodo e quindi fare clic su **Importa Management Pack**.  
  
    ![Fare clic su Importa Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  Nell'elenco dei management pack, selezionare il management pack che si desidera importare, fare clic su **selezionate**, quindi fare clic su **Add**.  
  
    ![Elenco dei Management pack](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Cercare **Appliance** e quindi il drill-down nella Base di Appliance di SQL Server e quindi fare clic su **Add** le due opzioni.  
  
    ![Base dello strumento di SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Dopo due Management Pack sono stati nel riquadro inferiore selezionato, quindi fare clic su **OK**.  
  
    ![Selezionare entrambi i management pack](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Fare clic su **Installa**.  
  
    ![Fare clic su Installa](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Al termine, fare clic su **Chiudi**.  
  
    ![Al termine, fare clic su Chiudi](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importare il Monitoring Pack per Microsoft SQL Server 2008 R2 Parallel Data Warehouse Appliance  
  
1.  Fare doppio clic il **Management Pack** nodo e quindi fare clic su **Importa Management Pack**.  
  
2.  Scegli **Aggiungi da disco**...  
  
    ![Fare clic sul Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Passare al percorso in cui sono stati estratti i Management Pack di SQL Server PDW e scegliere i tre management pack che sono disponibili nella sezione "Selected Management Pack eventualmente presenti per l'importazione". Questo scopo, seleziona il primo, facendo clic su MAIUSC e selezionare quello più recente. Una volta siano tutti selezionati, fare clic su **aperto**.  
  
    ![Selezionare i management pack](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Fare clic su **Installa**.  
  
    ![Fare clic su Installa](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Fare clic su **Chiudi**.  
  
    ![Fare clic su Chiudi](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Passaggio successivo  
Ora che sono stati importati i Management Pack, continuare al passaggio successivo: [Configurare SCOM per monitorare il sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
