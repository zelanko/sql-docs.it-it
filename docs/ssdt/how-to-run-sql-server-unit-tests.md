---
title: 'Procedura: Eseguire unit test di SQL Server | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b838503365dde968f938efb46c940f3a66ce4357
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098462"
---
# <a name="how-to-run-sql-server-unit-tests"></a>Procedura: Eseguire unit test di SQL Server
È possibile eseguire uno unit test di SQL Server in varie modalità, ad esempio usando diverse finestre e la finestra Prompt dei comandi.  
  
> [!NOTE]  
> Non è possibile eseguire unit test in modalità remota.  
  
Le modalità disponibili dipendono dal software installato, come descritto in [Esecuzione di unit test di SQL Server](../ssdt/running-sql-server-unit-tests.md).  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>Per eseguire unit test di SQL Server mediante Visualizzazione test (Visual Studio 2010)  
  
1.  Scegliere **Finestre** dal menu **Test**, quindi fare clic su **Visualizzazione test**.  
  
    Verrà visualizzata la finestra **Visualizzazione test**.  
  
2.  Nella finestra **Visualizzazione test** fare clic sui test da eseguire. Premere il tasto CTRL o MAIUSC per specificare blocchi contigui o non contigui di test.  
  
3.  Effettuare una delle operazioni seguenti:  
  
    -   Fare clic con il pulsante destro del mouse sulla superficie della finestra **Visualizzazione test**, quindi scegliere **Esegui selezione**.  
  
    -   Sulla barra degli strumenti **Visualizzazione test** fare clic su **Esegui selezione**.  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>Per eseguire unit test di SQL Server mediante Esplora test (Visual Studio 2012)  
  
1.  Scegliere **Finestre** dal menu **Test**, quindi fare clic su **Esplora test**.  
  
    Verrà visualizzata la finestra **Esplora test**.  
  
2.  In **Esplora test** fare clic sui test da eseguire. Premere il tasto CTRL o MAIUSC per specificare blocchi contigui o non contigui di test.  
  
3.  Fare clic con il pulsante destro del mouse sui test selezionati e quindi scegliere **Esegui test selezionati**.  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>Per eseguire unit test di SQL Server dalla finestra di progettazione unit test di SQL Server (Visual Studio 2010)  
  
-   Sulla barra degli strumenti **Strumenti di test** sono presenti i pulsanti per avviare un progetto con o senza debug.  
  
In questo passaggio vengono eseguiti tutti i test inclusi nell'esecuzione di test corrente. Non appena si avvia un'esecuzione di test, viene visualizzata la finestra **Risultati test** con lo stato dell'esecuzione di test. Nella visualizzazione sono inclusi i test in esecuzione e quelli completati. Per altre informazioni, vedere [Interpretazione dei risultati di unit test di SQL Server](../ssdt/interpreting-sql-server-unit-test-results.md).  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di unit test di SQL Server](../ssdt/running-sql-server-unit-tests.md)  
[Procedura: Eseguire test automatizzati da Microsoft Visual Studio 2010](https://msdn.microsoft.com/library/ms182470(VS.100).aspx)  
[Esecuzione di test automatizzati dalla riga di comando (Visual Studio 2010)](https://msdn.microsoft.com/library/ms182486(VS.100).aspx)  
[Test dell'applicazione (Visual Studio 2012)](https://msdn.microsoft.com/library/ms182409.aspx)  
  
