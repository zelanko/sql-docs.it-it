---
title: Opzioni (Editor di testo - XML - pagina formattazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97373178-d288-4127-af37-d9f5fe1b8607
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f96625c9658c3bd9864f0928e738357b6e14311e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089850"
---
# <a name="options-text-editor---xml---formatting-page"></a>Opzioni (Editor di testo - XML - pagina Formattazione)

Questa finestra di dialogo consente di specificare le impostazioni di formattazione per l'editor XML. È possibile accedere alla finestra di dialogo **Opzioni** dal menu **Strumenti**.  
  
> [!NOTE]  
> Queste impostazioni sono disponibili quando si selezionano la cartella **Editor di testo**, la cartella **XML** e quindi l'opzione **Formattazione** nella finestra di dialogo **Opzioni**.  
  
## <a name="attributes"></a>Attributi  
 **Mantieni la formattazione manuale degli attributi**  
 Consente di non riformattare gli attributi. Questa è l'impostazione predefinita.  
  
> [!NOTE]  
>  Se gli attributi sono disposti su più righe, a ogni riga di attributi verrà applicato un rientro corrispondente al rientro dell'elemento padre.  
  
 **Allinea ogni attributo su una riga separata**  
 Il secondo attributo e i successivi vengono allineati verticalmente in modo da corrispondere al rientro del primo attributo. Il testo XML seguente rappresenta un esempio del modo in cui gli attributi vengono allineati.  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95"  
</item>  
```  
  
## <a name="auto-reformat"></a>Riformatta automaticamente  
 **Quando si incolla dagli Appunti.**  
 Consente di riformattare il testo XML incollato dagli Appunti.  
  
 **Al completamento del tag di fine**  
 Consente di riformattare l'elemento al completamento del tag di fine.  
  
## <a name="mixed-content"></a>Contenuto misto  
 **Formatta contenuto misto per impostazione predefinita.**  
 Viene riformattato il contenuto misto, tranne quando il contenuto si trova in un ambito `xml:space="preserve"`. Questa è l'impostazione predefinita.  
  
 Se un elemento contiene testo e markup, il contenuto viene considerato misto. Di seguito viene riportato un esempio di elemento con contenuto misto.  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
```  
  
 \</dir>  
  
## <a name="see-also"></a>Vedere anche  
 [Editor XML &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)  
