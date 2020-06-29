---
title: Architettura degli oggetti server ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 33a8f420f985c9e62c7d7f275e7de370a6988e8d
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469056"
---
# <a name="adomdnet-server-object-architecture"></a>Architettura degli oggetti server in ADOMD.NET
  Gli oggetti del server ADOMD.NET sono oggetti helper che possono essere utilizzati per creare funzioni definite dall'utente o stored procedure in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Per utilizzare lo spazio dei nomi `Microsoft.AnalysisServices.AdomdServer` e tali oggetti, è necessario aggiungere un riferimento a msmgdsrv.dll nel progetto di una funzione definita dall'utente o di una stored procedure.  
  
 ![Relazioni tra gli oggetti nel componente server di ADOMD.NET](../../analysis-services/dev-guide/media/adomdnetserverobjectmodel.gif "Relazioni tra gli oggetti nel componente server di ADOMD.NET")  
Modello a oggetti ADOMD.NET  
  
 L'interazione con la gerarchia di oggetti ADOMD.NET viene avviata in genere con uno o più oggetti del livello più alto della gerarchia, come descritto nella tabella seguente.  
  
|A|Oggetto da utilizzare|  
|--------|---------------------|  
|Espressioni MDX (Multidimensional Expression)|[Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120))<br /> L'oggetto [Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) consente di eseguire un'espressione MDX e di valutare l'espressione in una tupla specificata.|  
|Supporto per l'esecuzione di funzioni MDX senza creare l'istruzione MDX completa|[Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120))<br /> L'oggetto [Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) è utile per chiamare funzioni MDX predefinite senza utilizzare l'oggetto [Microsoft. AnalysisServices. AdomdServer. Expression](/previous-versions/sql/sql-server-2014/ms143609(v=sql.120)) . Le funzioni aggiuntive per l'oggetto [Microsoft. AnalysisServices. AdomdServer. MDX](/previous-versions/sql/sql-server-2014/ms143616(v=sql.120)) devono essere disponibili nelle versioni future.|  
|Rappresentazione del contesto di esecuzione corrente per la funzione definita dall'utente|[Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))<br /> L'oggetto [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) espone informazioni quali il cubo corrente o il modello di data mining e varie raccolte di metadati. Un uso chiave dell'oggetto [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) è la proprietà [Microsoft. AnalysisServices. AdomdServer. Hierarchy. CurrentMember *](/previous-versions/sql/sql-server-2014/ms137044(v=sql.120)) dell'oggetto [Microsoft. AnalysisServices. AdomdServer. Hierarchy](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120)) . Tale utilizzo principale consente all'autore della funzione definita dall'utente o della stored procedure di prendere decisioni in base al membro di una dimensione specifica in cui si trova la query.|  
|Creazione di set e di tuple|[Microsoft. AnalysisServices. AdomdServer. Sebuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)), [Microsoft. AnalysisServices. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120))<br /> [Microsoft. AnalysisServices. AdomdServer. Sebuilder](/previous-versions/sql/sql-server-2014/ms144510(v=sql.120)) consente di creare set non modificabili, mentre [Microsoft. AnalysisServices. AdomdServer. TupleBuilder](/previous-versions/sql/sql-server-2014/ms145407(v=sql.120)) fornisce un modo per creare tuple non modificabili.|  
|Supporto della conversione implicita ed esecuzione del cast tra i sei tipi di base del linguaggio MDX|[Microsoft. AnalysisServices. AdomdServer. Toil](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120))<br /> L'oggetto [Microsoft. AnalysisServices. AdomdServer.](/previous-versions/sql/sql-server-2014/ms143573(v=sql.120)) toquesto fornisce la conversione implicita e il cast tra i tipi seguenti:<br /><br /> -   [Microsoft. AnalysisServices. AdomdServer. Hierarchy](/previous-versions/sql/sql-server-2014/ms143578(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Level](/previous-versions/sql/sql-server-2014/ms143581(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Member](/previous-versions/sql/sql-server-2014/ms143820(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. Tuple](/previous-versions/sql/sql-server-2014/ms145330(v=sql.120))<br />-   [Microsoft. AnalysisServices. AdomdServer. set](/previous-versions/sql/sql-server-2014/ms144530(v=sql.120))<br />-Scalare o tipi di valore|  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione di server ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
  
