---
title: Importa SCOM Management Pack
description: Seguire questa procedura per importare i Management Pack System Center Operations Manager (SCOM) per il sistema di piattaforma analitica (APS). I Management Pack sono necessari per monitorare i data warehouse paralleli da SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bcb0e667424767fd53a5fc7e027e84d512022203
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401078"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importare SCOM Management Pack-piattaforma Analytics System
Seguire questa procedura per importare i Management Pack System Center Operations Manager (SCOM) per il sistema di piattaforma analitica (APS). I Management Pack sono necessari per monitorare i data warehouse paralleli da SCOM. 
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>Prima di iniziare  
**Prerequisiti**  
  
System Center Operations Manager 2007 R2 deve essere installato e in esecuzione.  
  
È necessario installare i Management Pack. Vedere [Install the SCOM management packs &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md).  
  
## <a name="step-1-import-the-sql-server-appliance-base-management-pack"></a><a name="Step1"></a>Passaggio 1: importare il Management Pack di base SQL Server Appliance  
  
1.  Accedere al computer con un account che sia membro del ruolo Administrators di Operations Manager per il gruppo di gestione di Operations Manager 2007.  
  
2.  Nella Console operatore fare clic su **Amministrazione**.  
  
3.  Fare clic con il pulsante destro del mouse sul nodo **Management Pack** , quindi scegliere **Importa Management Pack**.  
  
    ![Fare clic su Importa Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  Nell'elenco dei Management Pack selezionare quello da importare, fare clic su **Seleziona**, quindi scegliere **Aggiungi**.  
  
    ![Elenco Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Cercare **Appliance** , quindi eseguire il drill-down nella base SQL Server Appliance, quindi fare clic su **Aggiungi** due opzioni.  
  
    ![Base dello strumento di SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Una volta che i due Management Pack si trovavano nel riquadro inferiore selezionato, fare clic su **OK**.  
  
    ![Selezionare entrambi i Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Fare clic su **Installa**.  
  
    ![Fare clic su Installa](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Al termine, fare clic su **Chiudi**.  
  
    ![Al termine fare clic su Chiudi](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="import-the-monitoring-pack-for-microsoft-sql-server-2008-r2-parallel-data-warehouse-appliance"></a><a name="Step2"></a>Importare il Monitoring Pack per 2008 Microsoft SQL Server Appliance data warehouse Parallel R2  
  
1.  Fare clic con il pulsante destro del mouse sul nodo **Management Pack** , quindi scegliere **Importa Management Pack**.  
  
2.  Scegliere **Aggiungi da disco**....  
  
    ![Fare clic con il pulsante destro del mouse su Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Passare al percorso in cui sono stati estratti i Management Pack SQL Server PDW e scegliere i tre Management Pack che si trovano nella sezione "Management Pack selezionati da importare". Questa operazione può essere eseguita selezionando la prima, facendo clic su Shift e selezionando l'ultima. Una volta selezionate tutte le selezioni, fare clic su **Apri**.  
  
    ![Seleziona Management Pack](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Fare clic su **Installa**.  
  
    ![Fare clic su Installa](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Fare clic su **Chiudi**.  
  
    ![Fare clic su Chiudi](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>passaggio successivo  
Ora che sono stati importati i Management Pack, procedere al passaggio successivo: [Configure SCOM to monitor Analytics Platform system &#40;Analytics Platform system&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
