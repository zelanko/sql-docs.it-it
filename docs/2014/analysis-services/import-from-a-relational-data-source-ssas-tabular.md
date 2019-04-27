---
title: Importare da un'origine dati relazionale (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 043201cc-fbef-4ed0-bde8-dc5e3a3e8bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44c4f0a5fbdaa64f2145113bf5135dad9acbddbb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730738"
---
# <a name="import-from-a-relational-data-source-ssas-tabular"></a>Importare da un'origine dati relazionale (SSAS tabulare)
  Tramite Importazione guidata tabella è possibile importare dati da un'ampia gamma di database relazionali. La procedura guidata è disponibile in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], dal menu **Modello** . Per connettersi a un'origine dati, è necessario che nel computer sia installato il provider appropriato. Per altre informazioni su origini dati e provider supportati, vedere [Data Sources Supported &#40;SSAS Tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
 L'Importazione guidata tabella supporta l'importazione di dati dalle origini dati seguenti:  
  
 **Database relazionali**  
  
-   Database di Microsoft SQL Server  
  
-   Microsoft SQL Azure  
  
-   Database di Microsoft Access  
  
-   Microsoft SQL Server Parallel Data Warehouse  
  
-   Oracle  
  
-   Teradata  
  
-   Sybase  
  
-   Informix  
  
-   IBM DB2  
  
-   OLE DB/ODBC  
  
 **Origini multidimensionali**  
  
-   Cubo di Microsoft SQL Server Analysis Services  
  
 L'Importazione guidata tabella non supporta l'importazione di dati da una cartella di lavoro di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] come origine dati.  
  
### <a name="to-import-data-from-a-database"></a>Per importare dati da un database  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modello** , quindi selezionare **Importa da origine dati**.  
  
2.  Nella pagina **Connessione a un'origine dati** selezionare il tipo di database a cui connettersi, quindi fare clic su **Avanti**.  
  
3.  Seguire i passaggi nell'Importazione guidata tabella. Nelle pagine successive, sarà possibile selezionare tabelle e viste specifiche o applicare filtri tramite la pagina **Selezione tabelle e viste** oppure creando una query SQL nella pagina **Specifica di una query SQL** .  
  
## <a name="see-also"></a>Vedere anche  
 [Importare dati &#40;SSAS tabulare&#41;](import-data-ssas-tabular.md)   
 [Origini dati supportate &#40;SSAS tabulare&#41;](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
