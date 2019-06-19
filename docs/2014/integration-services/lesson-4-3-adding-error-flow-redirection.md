---
title: 'Passaggio 3: Aggiunta del reindirizzamento del flusso di errore | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dd2fd95b1ad2d239d055b2b49b991860a58d338
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891403"
---
# <a name="step-3-adding-error-flow-redirection"></a>Passaggio 3: Aggiunta del reindirizzamento del flusso degli errori
  Come dimostrato nell'attività precedente, la trasformazione Lookup Currency Key non crea una corrispondenza quando tenta di elaborare il file flat di esempio danneggiato che ha generato un errore. Dato che la trasformazione utilizza le impostazioni predefinite per l'output degli errori, qualsiasi errore determina l'esito negativo della trasformazione. Quando la trasformazione viene interrotta, si interrompe anche il resto del pacchetto.  
  
 Anziché consentire la mancata riuscita della trasformazione, è possibile configurare il componente in modo da reindirizzare la riga con esito negativo a un altro percorso di elaborazione utilizzando l'output degli errori. L'utilizzo di un percorso di elaborazione separato per gli errori consente di ottenere diversi risultati. Ad esempio, è possibile ripulire i dati e quindi rielaborare la riga con esito negativo. È inoltre possibile salvare la riga con esito negativo insieme alle informazioni sugli errori aggiuntive in modo da consentire una verifica e una rielaborazione successive.  
  
 In questa attività si configurerà la trasformazione Lookup Currency Key in modo che le righe con esito negativo vengano reindirizzate all'output degli errori. Nel ramo del flusso di dati relativo agli errori, queste righe verranno scritte in un file.  
  
 Per impostazione predefinita, le due colonne supplementari in un output degli errori di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , ovvero **ErrorCode** e **ErrorColumn**, contengono solo codici numerici che rappresentano un numero di errore e l'ID della colonna in cui si è verificato l'errore. Questi valori numerici possono avere un'utilità limitata senza la descrizione dell'errore corrispondente.  
  
 Per aumentare l'utilità dell'output degli errori, prima che il pacchetto scriva le righe con esito negativo nel file è possibile utilizzare un componente script per accedere all'API di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e ottenere una descrizione dell'errore.  
  
### <a name="to-configure-an-error-output"></a>Per configurare un output degli errori  
  
1.  Nella **Casella degli strumenti SSIS**espandere **Comune**e trascinare **Componente script** sull'area di progettazione della scheda **Flusso di dati** . Posizionare **Script** a destra della trasformazione **Lookup Currency Key** .  
  
2.  Nella finestra di dialogo **Seleziona tipo componente script** fare clic su **Trasformazione**e quindi su **OK**.  
  
3.  Fare clic sulla trasformazione **Lookup Currency Key** e quindi trascinare la freccia rossa sulla trasformazione **Script** appena aggiunta per collegare i due componenti.  
  
     La freccia rossa rappresenta l'output degli errori della trasformazione **Lookup Currency Key** . Se si utilizza la freccia rossa per collegare la trasformazione al componente script è possibile reindirizzare qualsiasi errore di elaborazione al componente script, che successivamente elaborerà gli errori e li invierà alla destinazione.  
  
4.  Nella colonna **Errore** della finestra di dialogo **Configura output errori** selezionare **Reindirizza riga**e quindi fare clic su **OK**.  
  
5.  Nell'area di progettazione **Flusso di dati** fare clic su **Componente script** nel **Componente script**appena aggiunto e cambiare il nome in **Get Error Description**.  
  
6.  Fare doppio clic sulla trasformazione **Get Error Description** .  
  
7.  Nella pagina **Colonne di input** della finestra di dialogo **Editor trasformazione Script** selezionare la colonna **ErrorCode** .  
  
8.  Nella pagina **Input e output** espandere **Output 0**, fare clic su **Colonne di output**e fare clic su **Aggiungi colonna**.  
  
9. Nel `Name` proprietà, digitare **ErrorDescription** e impostare il `DataType` proprietà **stringa Unicode [DT_WSTR]** .  
  
10. Nel **Script** verificare che il `LocaleID` è impostata su **inglese (Stati Uniti.**  
  
11. Fare clic su **Modifica script** per aprire [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA). Nel metodo `Input0_ProcessInputRow` digitare o incollare il codice seguente.  
  
     [Visual Basic]  
  
    ```  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
     [Visual C#]  
  
    ```  
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
     La subroutine completa risulterà analoga al codice seguente.  
  
     [Visual Basic]  
  
    ```  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
     [Visual C#]  
  
    ```  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. Nel menu **Compila** fare clic su **Compila soluzione** per compilare lo script e salvare le modifiche, quindi chiudere VSTA.  
  
13. Scegliere **OK** per chiudere la finestra di dialogo **Editor trasformazione Script** .  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Passaggio 4: Aggiunta di una destinazione File Flat] (lesson-4-4-adding-a-flat-file-destination.md  
  
  
