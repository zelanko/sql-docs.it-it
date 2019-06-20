---
title: Uso di Microsoft SDK per Java | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 84c342150d00c399c4ab41c20d513b84f7be36db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701159"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Uso di Microsoft SDK per Java

> [!IMPORTANT]
> Microsoft non è più supportata di Visual J++ nel gennaio 2004.

Microsoft SDK per Java è kit per sviluppatori per l'ambiente di Microsoft Internet Explorer. Strumenti, informazioni ed esempi vengono forniti per lo sviluppo di applicazioni Java e applet basata 1.1 JDK e la macchina virtuale di Microsoft Win32 (Microsoft VM). Microsoft SDK per Java non è associato a Microsoft Visual J++. Per scaricare questo SDK, fare clic qui.  
  
 L'utilità Jactivex.exe genera classi da una libreria dei tipi, ma può essere richiamato solo sulla riga di comando. Questa funzionalità non è integrata con l'ambiente di sviluppo Visual J++. A differenza delle classi generate dalla procedura guidata libreria di tipo Java, è possibile eseguirne il wrapper della classe creato dal SDK. Ciò è utile per eseguire il debug come il codice utilizza le classi wrapper ADO.  
  
 Questo meccanismo legge la libreria dei tipi ADO e genera classi che è possibile creare un'istanza all'interno dell'applicazione. Genera le classi nel percorso seguente: \\< directory di windows\>\Java\trustlib\msado15.  
  
 Creazione di un'applicazione ADO in Java usando Microsoft SDK per Java è fondamentalmente identica, dalla prospettiva del codice sorgente, all'utilizzo della procedura guidata libreria di tipo Java. Per esempi di codice, vedere [wrapper di classe Java ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md). L'unica vera differenza è nella modalità di generazione di classi wrapper in primo luogo, come illustrato nei passaggi seguenti.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Per creare un progetto di ADO con Microsoft SDK per Java  
  
1.  Eseguire il comando seguente al prompt dei comandi. È necessario impostare il percorso per includere il SDK di Microsoft per la directory Bin di Java o eseguire il comando da quel percorso. In genere, Microsoft SDK per Java è installato nello stesso percorso di Visual Studio. Si tratta di un'istruzione singolo comando.  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  Eseguire il comando seguente per compilare le classi generate. Il commutatore /g: t attiva la generazione di simboli di debug in modo che sia possibile tenere traccia di. Simboli di Java. Rimuoverlo per le build di rilascio.  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  Per usare questi file, aprire il progetto in Visual J++. Dal **Project** menu, scegliere **Aggiungi a progetto**. Selezionare **file**e aggiungere tutte le. File JAVA generati nella directory trustlib\msado15 al progetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Wrapper di classe Java ADO](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
