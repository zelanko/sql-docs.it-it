---
title: 'Passaggio 3: Aggiunta del reindirizzamento del flusso degli errori | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e2c9e20ae26c3eec7069a20a09d54bd43836c0c9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440458"
---
# <a name="step-3-adding-error-flow-redirection"></a>Passaggio 3: Aggiunta del reindirizzamento del flusso degli errori
  Come dimostrato nell'attività precedente, la trasformazione Lookup Currency Key non crea una corrispondenza quando tenta di elaborare il file flat di esempio danneggiato che ha generato un errore. Dato che la trasformazione utilizza le impostazioni predefinite per l'output degli errori, qualsiasi errore determina l'esito negativo della trasformazione. Quando la trasformazione viene interrotta, si interrompe anche il resto del pacchetto.  
  
 Anziché consentire la mancata riuscita della trasformazione, è possibile configurare il componente in modo da reindirizzare la riga con esito negativo a un altro percorso di elaborazione utilizzando l'output degli errori. L'utilizzo di un percorso di elaborazione separato per gli errori consente di ottenere diversi risultati. Ad esempio, è possibile ripulire i dati e quindi rielaborare la riga con esito negativo. È inoltre possibile salvare la riga con esito negativo insieme alle informazioni sugli errori aggiuntive in modo da consentire una verifica e una rielaborazione successive.  
  
 In questa attività si configurerà la trasformazione Lookup Currency Key in modo che le righe con esito negativo vengano reindirizzate all'output degli errori. Nel ramo del flusso di dati relativo agli errori, queste righe verranno scritte in un file.  
  
 Per impostazione predefinita, le due colonne supplementari in un [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] output degli errori, **ErrorCode** e **ErrorColumn**, contengono solo codici numerici che rappresentano un numero di errore e l'ID della colonna in cui si è verificato l'errore. Questi valori numerici possono avere un'utilità limitata senza la descrizione dell'errore corrispondente.  
  
 Per aumentare l'utilità dell'output degli errori, prima che il pacchetto scriva le righe con esito negativo nel file è possibile utilizzare un componente script per accedere all'API di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e ottenere una descrizione dell'errore.  
  
### <a name="to-configure-an-error-output"></a>Per configurare un output degli errori  
  
1.  Nella **casella degli strumenti SSIS**espandere **comune**, quindi trascinare **componente script** sull'area di progettazione della scheda **flusso di dati** . Inserire **lo script** a destra della trasformazione **Lookup Currency Key** .  
  
2.  Nella finestra di dialogo **Seleziona tipo componente script** fare clic su **Trasformazione**e quindi su **OK**.  
  
3.  Fare clic sulla trasformazione **Lookup Currency Key** e quindi trascinare la freccia rossa sulla trasformazione **Script** appena aggiunta per collegare i due componenti.  
  
     La freccia rossa rappresenta l'output degli errori della trasformazione **Lookup Currency Key** . Se si utilizza la freccia rossa per collegare la trasformazione al componente script è possibile reindirizzare qualsiasi errore di elaborazione al componente script, che successivamente elaborerà gli errori e li invierà alla destinazione.  
  
4.  Nella colonna **Errore** della finestra di dialogo **Configura output errori** selezionare **Reindirizza riga**e quindi fare clic su **OK**.  
  
5.  Nell'area di progettazione **Flusso di dati** fare clic su **Componente script** nel **Componente script**appena aggiunto e cambiare il nome in **Get Error Description**.  
  
6.  Fare doppio clic sulla trasformazione **Get Error Description** .  
  
7.  Nella pagina **Colonne di input** della finestra di dialogo **Editor trasformazione Script** selezionare la colonna **ErrorCode** .  
  
8.  Nella pagina **Input e output** espandere **Output 0**, fare clic su **Colonne di output**e fare clic su **Aggiungi colonna**.  
  
9. Nella `Name` Proprietà digitare **ErrorDescription** e impostare la `DataType` proprietà su **stringa Unicode [DT_WSTR]**.  
  
10. Nella pagina **script** verificare che la `LocaleID` proprietà sia impostata su **inglese (Stati Uniti.**  
  
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
 [Passaggio 4: aggiunta di una destinazione file flat] (lesson-4-4-adding-a-flat-file-destination.md  
  
  
