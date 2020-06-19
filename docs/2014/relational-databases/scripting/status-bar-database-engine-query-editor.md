---
title: Barra di stato (editor di query del Motore di database)
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
author: rothja
ms.author: jroth
ms.openlocfilehash: 40c6c48e79d3694532aaf3651945488360d5ed50
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068485"
---
# <a name="status-bar-database-engine-query-editor"></a>Barra di stato (editor di query del Motore di database)
  La barra di stato delle finestre dell'editor di query di [!INCLUDE[ssDE](../../includes/ssde-md.md)] può apparire di colore diverso in modo da indicare a quale istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] è connessa ciascuna finestra.  
  
1.  **Prima di iniziare:**  [Colori della barra di stato](#StatusBarColors)  
  
2.  **Per impostare un colore di stato per un server in:**  [Esplora oggetti](#SetOEServerColor), [Server registrato](#SetRegServerColor)  
  
3.  **Per usare un colore di stato:**  [Aprire l'editor di query con un colore per il server](#OpenServerColor), [Aprire l'editor di query specificando un colore di stato](#OpenSpecColor)  
  
##  <a name="status-bar-colors"></a><a name="StatusBarColors"></a> Colori della barra di stato  
 È possibile associare un colore della barra di stato a uno specifico nodo server in **Esplora oggetti** o **Server registrati**. È possibile specificare i colori solo per nodi server connessi a un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)], non ai nodi server per altre tecnologie SQL Server. È inoltre possibile specificare anche un colore della barra di stato personalizzato ogni volta che si connette una nuova finestra dell'editor di query di [!INCLUDE[ssDE](../../includes/ssde-md.md)] a un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. È quindi possibile aprire una finestra dell'editor di query utilizzando il colore di stato definito per il nodo server oppure specificare un colore univoco per la finestra in questione.  
  
 L'impostazione di un colore della barra di stato personalizzato per un nodo server in Esplora oggetti deve essere effettuata al momento di effettuare la connessione. Per modificare il colore associato a un nodo server esistente, è necessario disconnettersi e quindi riconnettersi specificando il nuovo colore.  
  
##  <a name="set-the-status-color-for-a-server-in-object-explorer"></a><a name="SetOEServerColor"></a> Impostare il colore di stato per un server in Esplora oggetti  
 **Per impostare un colore di stato per un server in Esplora oggetti**  
  
1.  In **Esplora oggetti** fare clic sul pulsante **Connetti**, quindi selezionare **Motore di database...**  
  
2.  Nella finestra di dialogo **Connetti al server** selezionare **Opzioni >>** .  
  
3.  Selezionare la casella di controllo **Usa colore personalizzato** .  
  
4.  Per selezionare il colore, fare clic sul pulsante **Seleziona...**  
  
5.  Selezionare un colore di base o personalizzato, quindi scegliere OK.  
  
6.  Immettere le altre informazioni di connessione, quindi fare clic sul pulsante **Connetti** .  
  
##  <a name="set-the-status-color-for-a-registered-server"></a><a name="SetRegServerColor"></a> Impostare il colore di stato per un server registrato  
 **Per impostare il colore di stato per un server registrato**  
  
1.  In **Server registrati** fare clic con il pulsante destro del mouse sul nodo server desiderato, quindi scegliere **Proprietà...**  
  
2.  Nella finestra di dialogo **Modifica proprietà registrazione server** selezionare la scheda **Proprietà connessione** .  
  
3.  Selezionare la casella di controllo **Usa colore personalizzato** .  
  
4.  Per selezionare il colore, fare clic sul pulsante **Seleziona...**  
  
5.  Selezionare un colore di base o personalizzato, quindi scegliere OK.  
  
6.  Fare clic sul pulsante **Salva** nella finestra di dialogo **Modifica proprietà registrazione server** .  
  
##  <a name="open-an-editor-using-a-server-color"></a><a name="OpenServerColor"></a> Aprire un editor utilizzando un colore di server  
 **Per aprire una finestra di editor utilizzando un colore di server**  
  
-   Fare clic con il pulsante destro del mouse su un nodo server in **Esplora oggetti** o **Server registrati**, quindi scegliere **Nuova query**.  
  
-   In alternativa, evidenziare un nodo server, quindi fare clic sul pulsante **Nuova query** della barra degli strumenti.  
  
-   La barra di stato della finestra dell'editor utilizzerà il colore definito per il server associato.  
  
##  <a name="open-an-editor-specifying-a-status-color"></a><a name="OpenSpecColor"></a> Aprire un editor specificando un colore di stato  
 **Per aprire una finestra di editor specificando un colore di stato**  
  
-   Scegliere **Nuovo** dal menu **File**, quindi selezionare **Query del motore di database**.  
  
-   Nella finestra di dialogo **Connetti al server** selezionare **Opzioni >>** .  
  
-   Selezionare la casella di controllo **Usa colore personalizzato** .  
  
-   Per selezionare il colore, fare clic sul pulsante **Seleziona...**  
  
-   Selezionare un colore di base o personalizzato, quindi scegliere OK.  
  
-   Immettere le altre informazioni di connessione, quindi fare clic sul pulsante **Connetti** .  
  
## <a name="see-also"></a>Vedere anche  
 [Editor di query e di testo &#40;SQL Server Management Studio&#41;](../scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
