---
title: Finestra di messaggio eccezione programma | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316afc6d5f3a87ff7431240681066ac5ee66ede6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62780697"
---
# <a name="program-exception-message-box"></a>Programmare la finestra di messaggio eccezione
  È possibile usare la finestra di messaggio eccezione nelle applicazioni per offrire un controllo maggiore sull'invio e la ricezione di messaggi rispetto a quello garantito dalla classe <xref:System.Windows.Forms.MessageBox>. Per ulteriori informazioni, vedere la pagina relativa alla [programmazione della finestra di messaggio eccezione](../../../2014/database-engine/dev-guide/exception-message-box-programming.md). Per informazioni su come ottenere e distribuire il file dll della finestra di messaggio eccezione, vedere [Deploying an Exception Message Box Application](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md).  
  
## <a name="procedure"></a>Procedura  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>Per gestire un'eccezione tramite la finestra di messaggio eccezione  
  
1.  Aggiungere un riferimento all'assembly Microsoft.ExceptionMessageBox.dll nel progetto di codice gestito.  
  
2.  Opzionale Aggiungere una `using` direttiva (C#) `Imports` o[!INCLUDE[msCoName](../../includes/msconame-md.md)] (Visual Basic .NET) per usare lo <xref:Microsoft.SqlServer.MessageBox> spazio dei nomi.  
  
3.  Creare un blocco Try-Catch per gestire l'eccezione anticipata.  
  
4.  All'interno del blocco `catch` creare un'istanza della classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>. Passare l' <xref:System.Exception> oggetto gestito dal `try` - `catch` blocco.  
  
5.  (Facoltativo) Impostare una o più delle proprietà seguenti su <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons>Enumerazione che specifica i pulsanti da visualizzare nella finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton>Enumerazione che specifica il pulsante predefinito per la finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions>Enumerazione utilizzata per controllare altri comportamenti della finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol>Enumerazione che specifica il simbolo da visualizzare nella finestra di messaggio eccezione.  
  
6.  Chiamare il metodo <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . Passare la finestra padre alla quale appartiene la finestra di messaggio eccezione.  
  
7.  (Facoltativo) Annotare il valore dell'enumerazione <xref:System.Windows.Forms.DialogResult> restituita se è necessario determinare su quale pulsante l'utente ha fatto clic.  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>Per visualizzare la finestra di messaggio eccezione senza un'eccezione  
  
1.  Aggiungere un riferimento all'assembly Microsoft.ExceptionMessageBox.dll nel progetto di codice gestito.  
  
2.  Opzionale Aggiungere una `using` direttiva (C#) `Imports` o (Visual Basic .NET) per usare lo <xref:Microsoft.SqlServer.MessageBox> spazio dei nomi.  
  
3.  Creare un'istanza della classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>. Passare il testo del messaggio come valore <xref:System.String>.  
  
4.  (Facoltativo) Impostare una o più delle proprietà seguenti su <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons>Enumerazione che specifica i pulsanti da visualizzare nella finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A>: didascalia della finestra di dialogo della finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton>Enumerazione che specifica il pulsante predefinito per la finestra di dialogo della finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions>Enumerazione utilizzata per controllare altri comportamenti della finestra di messaggio eccezione.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol>Enumerazione che specifica il simbolo da visualizzare nella finestra di messaggio eccezione.  
  
5.  Chiamare il metodo <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . Passare la finestra padre alla quale appartiene la finestra di messaggio eccezione.  
  
6.  (Facoltativo) Annotare il valore dell'enumerazione <xref:System.Windows.Forms.DialogResult> restituita se è necessario determinare su quale pulsante l'utente ha fatto clic.  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>Per visualizzare la finestra di messaggio eccezione con pulsanti personalizzati  
  
1.  Aggiungere un riferimento all'assembly Microsoft.ExceptionMessageBox.dll nel progetto di codice gestito.  
  
2.  Opzionale Aggiungere una `using` direttiva (C#) `Imports` o (Visual Basic .NET) per usare lo <xref:Microsoft.SqlServer.MessageBox> spazio dei nomi.  
  
3.  Creare un'istanza della classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> in uno dei due modi seguenti:  
  
    -   Passare l' <xref:System.Exception> oggetto gestito da un `try` - `catch` blocco.  
  
    -   Passare il testo del messaggio come valore <xref:System.String>.  
  
4.  Impostare uno dei seguenti valori per <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore>-Visualizza i pulsanti **Interrompi**, **Riprova**e **Ignora** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom>: visualizza pulsanti personalizzati.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK>-Visualizza il pulsante **OK** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel>: Visualizza i pulsanti **OK** e **Annulla** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel>: Visualizza i pulsanti **Riprova** e **Annulla** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo>: Visualizza i pulsanti **Sì** e **No** .  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel>: Visualizza i pulsanti **Sì**, **No**e **Annulla** .  
  
5.  (Facoltativo) Se si usano pulsanti personalizzati, chiamare uno degli overload del metodo <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> per specificare il testo per un massimo di cinque pulsanti personalizzati.  
  
6.  Chiamare il metodo <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . Passare la finestra padre alla quale appartiene la finestra di messaggio eccezione.  
  
7.  (Facoltativo) Annotare il valore dell'enumerazione <xref:System.Windows.Forms.DialogResult> restituita se è necessario determinare su quale pulsante l'utente ha fatto clic. Se si usano pulsanti personalizzati, annotare il valore di <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> per la proprietà <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> per determinare su quale pulsante personalizzato l'utente ha fatto clic.  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>Per consentire agli utenti di decidere se visualizzare la finestra di messaggio eccezione  
  
1.  Aggiungere un riferimento all'assembly Microsoft.ExceptionMessageBox.dll nel progetto di codice gestito.  
  
2.  Opzionale Aggiungere una `using` direttiva (C#) `Imports` o (Visual Basic .NET) per usare lo <xref:Microsoft.SqlServer.MessageBox> spazio dei nomi.  
  
3.  Creare un'istanza della classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> in uno dei due modi seguenti:  
  
    -   Passare l' <xref:System.Exception> oggetto gestito da un `try` - `catch` blocco.  
  
    -   Passare il testo del messaggio come valore <xref:System.String>.  
  
4.  Impostare la proprietà <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> su `true`.  
  
5.  (Facoltativo) Specificare il testo per chiedere all'utente di decidere se visualizzare nuovamente la finestra di messaggio eccezione per <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>. Il testo predefinito è "Non visualizzare più questo messaggio".  
  
6.  Se è necessario mantenere la decisione dell'utente solo per la durata dell'esecuzione dell'applicazione, impostare il valore di <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> su una variabile <xref:System.Boolean> globale. Valutare questo valore prima di creare un'istanza della finestra di messaggio eccezione.  
  
7.  Se è necessario archiviare in modo permanente la decisione di un utente, eseguire le operazioni seguenti:  
  
    1.  Chiamare il metodo CreateSubKey per aprire una chiave del Registro di sistema personalizzata usata dall'applicazione e impostare <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> sull'oggetto RegistryKey restituito.  
  
    2.  Impostare <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> sul nome del valore del Registro di sistema usato.  
  
    3.  Impostare <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> su `true`.  
  
    4.  Chiamare il metodo <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . La chiave del Registro di sistema specificata viene valutata e la finestra di messaggio eccezione viene visualizzata solo se i dati archiviati in tale chiave sono pari a 0. Se la finestra di dialogo viene visualizzata e l'utente seleziona la casella di controllo prima di fare clic su un pulsante, i dati nella chiave del Registro di sistema vengono impostati su 1.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene usata la finestra di messaggio eccezione con il pulsante **OK** per visualizzare le informazioni di un'eccezione dell'applicazione che include l'eccezione gestita insieme ad altre informazioni specifiche dell'applicazione.  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>Esempio  
 In questo esempio viene usata la finestra di messaggio eccezione con i pulsanti **Sì** e **No** da cui l'utente sceglie.  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>Esempio  
 In questo esempio viene usata la finestra di messaggio eccezione con pulsanti personalizzati.  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>Esempio  
 In questo esempio viene usata la casella di controllo per determinare se visualizzare la finestra di messaggio eccezione.  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>Esempio  
 In questo esempio vengono usate la casella di controllo e una chiave del Registro di sistema per determinare se visualizzare la finestra di messaggio eccezione.  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>Esempio  
 In questo esempio viene usata la finestra di messaggio eccezione per visualizzare informazioni aggiuntive utili per la risoluzione dei problemi o il debug.  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
