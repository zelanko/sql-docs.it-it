---
title: Generare script
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9f97b1682fa8a2e04b5f1afcc2a552a326a9e43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75242095"
---
# <a name="generate-scripts-sql-server-management-studio"></a>Generazione di script (SQL Server Management Studio)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornisce due meccanismi per la generazione di script [!INCLUDE[tsql](../../includes/tsql-md.md)] . È possibile creare script per più oggetti utilizzando la **procedura guidata genera e pubblica script.** È anche possibile generare uno script per un singolo oggetto o per più oggetti usando il menu **Crea script per** in **Esplora oggetti**.  
  
1.  **Scegliere un metodo:**  [procedura guidata genera e pubblica script](#GenPubScriptWiz), [Esplora oggetti script come menu](#OEScriptAsMenu)  
  
2.  **Per usare il menu script come:**  [creare uno script per un singolo oggetto](#ScriptSingleObject), [creare uno script per due oggetti usando Esplora oggetti](#ScriptTwoObjectsOE), [creare uno script per due oggetti usando Esplora oggetti dettagli](#ScriptTwoObjectsOED)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Scegliere il meccanismo che soddisfa maggiormente i requisiti.  
  
###  <a name="GenPubScriptWiz"></a> Procedura guidata Genera e pubblica script  
 Usare la **Procedura guidata Genera e pubblica script** per creare uno script [!INCLUDE[tsql](../../includes/tsql-md.md)] per molti oggetti. Durante la procedura guidata viene generato uno script di tutti gli oggetti contenuti in un database o un subset degli oggetti selezionati. La procedura guidata dispone di numerose opzioni per gli script, che consentono ad esempio di includere autorizzazioni, regole di confronto, vincoli e così via. Per istruzioni sull'uso della procedura guidata, vedere [Genera e pubblica script](generate-and-publish-scripts-wizard.md).  
  
###  <a name="OEScriptAsMenu"></a> Menu Crea script per in Esplora oggetti  
 Il menu **Crea script per in Esplora oggetti** consente di creare uno script per un solo oggetto, più oggetti o più istruzioni per un singolo oggetto. È possibile scegliere tra diversi tipi di script, per ad esempio creare, modificare o eliminare l'oggetto. È possibile salvare lo script in una finestra dell'editor di query, in un file o negli Appunti. Lo script viene creato in formato Unicode.  
  
##  <a name="ScriptSingleObject"></a> Per generare uno script per un singolo oggetto  
 **Per generare uno script per un singolo oggetto**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, quindi espandere il database che contiene l'oggetto per cui creare lo script.  
  
3.  Espandere la categoria dell'oggetto: ad esempio il nodo **Tabelle** o **Viste** .  
  
4.  Fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Crea script per \<tipo di oggetto**, ad esempio **Crea script per tabella**.  
  
5.  Scegliere il tipo di script, ad esempio **Genera codice per istruzione CREATE** o **Genera codice per istruzione ALTER**.  
  
6.  Selezionare il percorso in cui salvare lo script, ad esempio **Nuova finestra editor di query** o **Appunti**.  
  
##  <a name="ScriptTwoObjectsOE"></a>Per generare uno script di due oggetti usando Esplora oggetti  
 **Per creare uno script per due oggetti usando Esplora oggetti**  
  
 Talvolta può essere necessario creare uno script con più opzioni, ad esempio per eliminare una procedura e successivamente crearne un'altra o per creare e quindi modificare una tabella. I processi riportati di seguito per la generazione di script di più oggetti, possono essere utilizzato anche quando è necessario creare uno script che fa riferimento a tipi diversi di oggetti, quali tabelle, viste e stored procedure.  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, quindi espandere il database che contiene gli oggetti per cui creare lo script.  
  
3.  Fare clic con il pulsante destro del mouse sul primo oggetto per cui generare lo script, scegliere Crea ** \<script per tipo di oggetto>** e nelle selezioni **Salva con nome** scegliere **nuova finestra Editor di query** come destinazione dell'output.  
  
4.  Passare al secondo oggetto per cui si desidera creare lo script.  
  
5.  Fare clic con il pulsante destro del mouse sull'oggetto, scegliere Crea **script \<per tipo di oggetto>** e nelle selezioni **Salva con nome** scegliere **Appunti** come destinazione dell'output.  
  
6.  Nella finestra dell'editor di query aperta per il primo oggetto incollare lo script per il secondo oggetto dagli Appunti.  
  
##  <a name="ScriptTwoObjectsOED"></a>Per generare uno script di due oggetti usando Esplora oggetti dettagli  
 **Per creare uno script per due oggetti usando Esplora oggetti dettagli**  
  
 È possibile usare il riquadro **Dettagli Esplora oggetti** per generare uno script per più oggetti della stessa categoria.  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , quindi espandere questa istanza.  
  
2.  Espandere **Database**, quindi espandere il database che contiene gli oggetti per cui creare lo script.  
  
3.  Espandere il nodo della categoria dei tipi di oggetto per cui si vuole creare uno script, ad esempio il nodo **Tabelle** .  
  
4.  Aprire il riquadro **Dettagli Esplora oggetti** premendo il tasto **F7**oppure selezionando **Dettagli Esplora oggetti** dal menu **Visualizza**.  
  
5.  Fare clic su uno degli oggetti per cui si desidera creare lo script.  
  
6.  Tenendo premuto il tasto Crtl fare clic sul secondo oggetto per cui si desidera creare lo script.  
  
7.  Fare clic con il pulsante destro del mouse su uno degli oggetti selezionati e scegliere **Crea script per \<tipo di oggetto>** .  
  
  
