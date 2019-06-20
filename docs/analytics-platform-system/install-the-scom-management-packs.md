---
title: Installare i management pack SCOM - sistema di piattaforma Analitica | Microsoft Docs
description: Seguire questi passaggi per scaricare e installare i Management Pack di System Center Operations Manager (SCOM) per SQL Server PDW. I Management Pack sono necessari per monitorare SQL Server PDW da SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f0acfa636a3432dcffb18cfec57ee7625c1eb01b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63215587"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Installare SQL Server Operations Manager (SCOM) management pack per sistema di piattaforma Analitica
Seguire questi passaggi per scaricare e installare i Management Pack di System Center Operations Manager (SCOM) per SQL Server PDW. I Management Pack sono necessari per monitorare SQL Server PDW da SCOM.  
  
## <a name="BeforeBegin"></a>Prima di iniziare  
**Prerequisiti**  
  
System Center Operations Manager deve essere installato e in esecuzione. SQL Server 2012 PDW richiede System Center Operations Manager 2007 R2, System Center Operations Manager 2012 o System Center Operations Manager 2012 service pack 1.  
  
## <a name="Step1"></a>Passaggio 1: Scaricare i Management Pack  
Per il carico di lavoro di PDW APS, scaricare il [Management Pack di System Center per il sistema di piattaforma Analitica Microsoft](https://go.microsoft.com/fwlink/?LinkId=396857).  
  
Per la gestione di appliance, scaricare il [Base Management Pack di SQL Server Appliance](https://www.microsoft.com/download/details.aspx?displaylang=en&id=11436).  
  
Per le versioni precedenti di PDW senza punti di accesso, scaricare il[System Center Monitoring Pack per Microsoft SQL Server 2012 Parallel Data Warehouse Appliance](https://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>Passaggio 2: Installare i Management Pack  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>Installare il Base Management Pack SQL Server Appliance  
  
1.  Per eseguire l'installazione, fare doppio clic sul Management Pack scaricato SQL Server Appliance Base.  
  
2.  Accettare il contratto di licenza e fare clic su **successivo**.  
  
    ![Accettare il contratto di licenza](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  Selezionare la propria cartella di installazione oppure utilizzare il cartella di installazione di Management Pack predefinito.  
  
    ![Selezione cartella di installazione](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  Fare clic su **Installa**.  
  
    ![Confermare l'installazione](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  Scegliere **Chiudi**.  
  
    ![Fare clic su Chiudi](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>Installare il Monitoring Pack per SQL Server PDW Appliance  
  
1.  Per eseguire l'installazione, fare doppio clic sul Management Pack scaricato SQL Server PDW Appliance.  
  
2.  Accettare il contratto di licenza e fare clic su **successivo**.  
  
    ![Accettare il contratto di licenza](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  Scegliere la directory che conterrà i file estratti. La cartella di installazione di Management Pack predefinito viene visualizzata per impostazione predefinita. Selezionare l'impostazione predefinita, oppure selezionare la propria cartella di installazione.  
  
    ![Selezione cartella di installazione](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Fare clic su **Installa**.  
  
    ![Confermare l'installazione](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Scegliere **Chiudi**.  
  
    ![Installazione completata](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Passaggio successivo  
Dopo aver creato il Management Pack installati, continuare al passaggio successivo: [Importare il Management Pack SCOM per PDW &#40;sistema di piattaforma Analitica&#41;](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
