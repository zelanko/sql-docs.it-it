---
title: Individuare la versione dello schema di definizione del report (SSRS) | Microsoft Docs
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 129fcb8e1533162560b88e9400c68c7c863be119
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826834"
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>Individuare la versione dello schema di definizione del report (SSRS)

Un file di definizione del report specifica lo spazio dei nomi RDL per la versione dello schema di definizione del report utilizzata per convalidare il file rdl. Quando si apre un file con estensione RDL in un ambiente, ad esempio Progettazione Report di creazione report [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], Visual Studio o Generatore Report. Se il report è stato creato per uno spazio dei nomi precedente, viene creato automaticamente un file di backup e il report viene aggiornato allo spazio dei nomi corrente. Salvando la definizione del report aggiornata, si salva il file con estensione rdl convertito. Questo è l'unico modo per aggiornare una definizione del report. La definizione del report non viene aggiornata su un server di report. Il report compilato viene aggiornato su un server di report. Per altre informazioni, vedere [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
## <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>Procedura: Identificare la versione di schema RDL di un report  
  
1. Aprire il file del report con estensione rdl in un'applicazione, ad esempio il Blocco note o XML Notepad, nella quale è possibile visualizzare il codice XML.  
  
     L'elemento Report XML specifica lo spazio dei nomi dello schema. L'elemento Report seguente, ad esempio, specifica lo spazio dei nomi per Progettazione report e lo spazio dei nomi per la definizione del report.  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     Lo spazio dei nomi definizione di report più recente è il 2016. Tuttavia, lo spazio dei nomi definizione di report pubblicato più recente è 2010, specificato dall'URL seguente: `https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`...
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>Procedura: Identificare la versione di schema RDL di Progettazione report  
  
1.  Apre un nuovo progetto. La versione del progetto che si sceglie determina la versione dello schema RDL. In SQL Server sono supportate più versioni dello schema. Per altre informazioni, vedere [Distribuzione e supporto della versione in SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  Dal menu **Progetto** fare clic su **Aggiungi nuovo elemento**. Verrà visualizzata la finestra di dialogo **Aggiungi nuovo elemento** .  
  
3.  Nel riquadro **Modelli** fare clic su **Report**.  
  
4.  In **Nome**digitare un nome di report o accettare il nome predefinito.  
  
5.  Scegliere **Aggiungi**. Progettazione report apre un nuovo report vuoto nella visualizzazione della struttura.  
  
6.  Scegliere **Codice** dal menu **Visualizza**. La definizione del report viene visualizzata come file XML.  
  
    L'elemento Report XML specifica lo spazio dei nomi dello schema. L'elemento Report seguente, ad esempio, specifica lo spazio dei nomi per Progettazione report e lo spazio dei nomi per la definizione del report.  
  
    ``` XML 
    <Report xmlns:rd="http://schemas.microsoft.com/SQLServer/reporting/reportdesigner" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" xmlns:df="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition/defaultfontfamily" MustUnderstand="df">  
    ```  
  
     Lo spazio dei nomi della definizione del report viene specificato dall'URL seguente: `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>Procedura: Identificare la versione di schema RDL nel server di report  
  
-   Nel portale web, digitare l'URL del server di report. Ad esempio, nel seguente URL viene specificato un server di report sul computer locale:  
  
     `https://localhost/reportserver/reportdefinition.xsd`  
  
     Il file con estensione xsd viene aperto nel browser.  
  
     L'elemento XML Schema specifica lo spazio dei nomi dello schema. Nell'elemento schema seguente, ad esempio, sono specificati tre spazi dei nomi: il riferimento di targetNamespace usato internamente da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], il riferimento xsd per lo schema stesso (xsd) e il riferimento della definizione del report.  *Anno* rappresenta l'anno dello schema è utilizzando il report. Ad esempio, 2010 o 2016.
  
    ``` XML  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition" elementFormDefault="qualified">  
    ```  
  
     Lo spazio dei nomi della definizione del report viene specificato dall'URL seguente: `https://schemas.microsoft.com/sqlserver/reporting/*year*/01/reportdefinition`  

## <a name="next-steps"></a>Passaggi successivi
[Aggiornare i report](../../reporting-services/install-windows/upgrade-reports.md)   
[Report Definition Language](../../reporting-services/reports/report-definition-language-ssrs.md)   

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
