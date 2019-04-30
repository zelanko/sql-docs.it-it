---
title: Individuare la versione dello schema di definizione del report (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3306160d1badb4abb1f173071f07bde514f5fc1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224740"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>Individuare la versione dello schema di definizione del report (SSRS)
  Un file di definizione del report specifica lo spazio dei nomi RDL per la versione dello schema di definizione del report utilizzata per convalidare il file rdl. Quando si apre un file con estensione rdl in un ambiente di creazione di report, ad esempio Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o Generatore report, se il report è creato per uno spazio dei nomi precedente, viene automaticamente creato un file di backup e il report viene aggiornato allo spazio dei nomi corrente. Salvando la definizione del report aggiornata, si salva il file con estensione rdl convertito. Questo è l'unico modo per aggiornare una definizione del report. La definizione del report non viene aggiornata su un server di report. Il report compilato viene aggiornato su un server di report. Per altre informazioni, vedere [Upgrade Reports](../install-windows/upgrade-reports.md).  
  
### <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>Procedura: Identificazione della versione di schema RDL di un report  
  
1.  Aprire il file del report con estensione rdl in un'applicazione, ad esempio Blocco note o XML Blocco note 2007, nella quale è possibile visualizzare file in formato xml.  
  
     L'elemento Report XML specifica lo spazio dei nomi dello schema. L'elemento Report seguente, ad esempio, specifica lo spazio dei nomi per Progettazione report e lo spazio dei nomi per la definizione del report.  
  
    ```  
    <Report xmlns:rd=https://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     Lo spazio dei nomi della definizione del report viene specificato dall'URL seguente: `https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`.  
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>Procedura: Identificazione della versione di schema RDL di Progettazione report  
  
1.  Apre un nuovo progetto. La versione del progetto che si sceglie determina la versione dello schema RDL. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sono supportate più versioni dello schema. Per altre informazioni, vedere [Distribuzione e supporto della versione in SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  Dal menu **Progetto** fare clic su **Aggiungi nuovo elemento**. Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento** .  
  
3.  Nel riquadro **Modelli** fare clic su **Report**.  
  
4.  In **Nome**digitare un nome di report o accettare il nome predefinito.  
  
5.  Scegliere **Aggiungi**. Progettazione report apre un nuovo report vuoto nella visualizzazione della struttura.  
  
6.  Scegliere **Codice** dal menu **Visualizza**. La definizione del report viene visualizzata come file XML.  
  
     L'elemento Report XML specifica lo spazio dei nomi dello schema. L'elemento Report seguente, ad esempio, specifica lo spazio dei nomi per Progettazione report e lo spazio dei nomi per la definizione del report.  
  
    ```  
    <Report xmlns:rd=https://schemas.microsoft.com/SQLServer/reporting/reportdesigner  
    xmlns="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     Lo spazio dei nomi della definizione del report viene specificato dall'URL seguente: `https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>Procedura: Identificazione della versione di schema RDL nel server di report  
  
-   In Gestione report digitare l'URL per il server di report. Ad esempio, nel seguente URL viene specificato un server di report sul computer locale:  
  
     `http://localhost/reportserver/reportdefinition.xsd`  
  
     Il file con estensione xsd viene aperto nel browser.  
  
     L'elemento XML Schema specifica lo spazio dei nomi dello schema. Nell'elemento schema seguente, ad esempio, sono specificati tre spazi dei nomi: il riferimento di targetNamespace usato internamente da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], il riferimento xsd per lo schema stesso (xsd) e il riferimento della definizione del report.  
  
    ```  
    <xsd:schema   
    targetNamespace="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
    xmlns="https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    elementFormDefault="qualified">  
    ```  
  
     Lo spazio dei nomi della definizione del report viene specificato dall'URL seguente: `https://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
## <a name="see-also"></a>Vedere anche  
 [Upgrade Reports](../install-windows/upgrade-reports.md)   
 [Report Definition Language &#40;SSRS&#41;](report-definition-language-ssrs.md)  
  
  
