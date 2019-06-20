---
title: Pianificazione dell'aggiornamento dati e origini dati che non supportano l'autenticazione di Windows (PowerPivot per SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d8d875bc-7823-46b7-a939-867cefd4de12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4851c8054434713e69d8bf63b046484a01f0398
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071161"
---
# <a name="schedule-data-refresh-and-data-sources-that-do-not-support-windows-authentication-powerpivot-for-sharepoint"></a>Pianificazione dell'aggiornamento dati e origini dati che non supportano l'autenticazione di Windows (PowerPivot per SharePoint)
  Questo argomento descrive un flusso di lavoro della pianificazione di un aggiornamento dati di PowerPivot per SharePoint in cui è possibile usare origini dati che **NON** supportano l'autenticazione di Windows, ad esempio origini dati Oracle o IDM DB2. Le illustrazioni e i passaggi presenti in questo argomento fanno riferimento alle origini dati Oracle ma lo stesso flusso di lavoro è valido anche per altre origini dati.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010 &#124; SharePoint 2013.|  
  
 **Panoramica:** Creare due Secure Store le applicazioni di destinazione. Configurare la prima applicazione di destinazione (PowerPivotDataRefresh) per l'utilizzo delle credenziali Windows. Configurare la seconda applicazione di destinazione con le credenziali di un'origine dati che non supporta l'autenticazione di Windows, ad esempio un database Oracle. La seconda applicazione di destinazione utilizza anche la prima applicazione di destinazione per l'account di aggiornamento dati automatico.  
  
 ![as_powerpivot_refresh_no_windows_auth](../media/as-powerpivot-refresh-no-windows-auth.gif "as_powerpivot_refresh_no_windows_auth")  
  
-   **(1) PowerPivotDatarefresh:** Una Secure Store ID applicazione di destinazione impostato con l'autenticazione di windows.  
  
-   **(2) OracleAuthentication:** Una Secure Store ID applicazione di destinazione impostato con le credenziali Oracle.  
  
-   **(3)**  Applicazione del servizio PowerPivot viene configurata per usare l'applicazione di destinazione "PowerPivotDataRefresh" per il **Account di aggiornamento dati automatico**.  
  
-   **(4)** Cartella di lavoro PowerePivot con dati Oracle. Le impostazioni di aggiornamento della cartella di lavoro specificano la connessione all'origine dati in modo da usare l'applicazione di destinazione **(2)** per le credenziali.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   Applicazione di servizio PowerPivot esistente  
  
-   Applicazione del servizio di archiviazione sicura esistente  
  
-   Cartella di lavoro di Excel con modello di dati PowerPivot esistente  
  
## <a name="to-create-a-target-application-id-that-uses-windows-authentication"></a>Per creare un ID applicazione di destinazione che utilizza l'autenticazione di Windows  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione del servizio di archiviazione sicura.  
  
3.  Nella pagina **Gestione** fare clic su **Nuovo**. ![as_powerpivot_refresh_sss_new_target_application](../media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application")  
  
4.  Nella pagina **Crea nuova applicazione di destinazione dell'archiviazione sicura** configurare i valori seguenti:  
  
    -   **ID applicazione di destinazione:** PowerPivotDataRefresh.  
  
    -   **Nome visualizzato:** PowerPivotDataRefresh.  
  
    -   **Posta elettronica contatto:** ?  
  
    -   **Tipo di applicazione di destinazione:** gruppo.  
  
    -   **URL pagina di destinazione dell'applicazione:** Nessuna.  
  
5.  Scegliere **Avanti**.  
  
6.  Nella pagina Credenziali lasciare i due nomi di campo e tipi di campo predefiniti per **Nome utente Windows** e **Password Windows**.  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina **Impostazioni di appartenenza** aggiungere almeno un **Amministratore dell'applicazione di destinazione** e quindi aggiungere i membri che richiedono l'accesso all'applicazione di destinazione.  
  
9. Fare clic su **OK**.  
  
10. Il nuovo ID applicazione di destinazione verrà aggiunto all'elenco. Selezionare l'ID applicazione di destinazione e fare clic su **impostare le credenziali**![as_powerpivot_refresh_sss_set_key](../media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key").  
  
11. Digitare il Nome utente Windows e la Password Windows e quindi fare clic su **OK**.  
  
## <a name="to-create-a-target-application-id-that-uses-oracle-credentials"></a>Per creare un ID applicazione di destinazione che utilizza le credenziali Oracle  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione del servizio di archiviazione sicura.  
  
3.  Nel **Manage** pagina, fare clic su **New**![as_powerpivot_refresh_sss_new_target_application](../media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application ").  
  
4.  Nella pagina **Crea nuova applicazione di destinazione dell'archiviazione sicura** configurare i valori seguenti:  
  
    -   **ID applicazione di destinazione:** OracleAuthentication.  
  
    -   **Nome visualizzato:** OracleAuthentication.  
  
    -   **Posta elettronica contatto:** ?  
  
    -   **Tipo di applicazione di destinazione:** gruppo.  
  
    -   **URL pagina di destinazione dell'applicazione:** Nessuna.  
  
5.  Scegliere **Avanti**.  
  
6.  Nel **credenziali** pagina, modificare il nome del primo campo `Oracle User ID` e modificare le **tipo di campo** a `User Name`.  
  
     Modificare il secondo nome di campo in `Oracle Password` e il **tipo di campo** a `Password`.  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina **Impostazioni di appartenenza** aggiungere almeno un **Amministratore dell'applicazione di destinazione** e quindi aggiungere i membri che richiedono l'accesso all'applicazione di destinazione.  
  
9. Fare clic su **OK**.  
  
10. Il nuovo ID applicazione di destinazione verrà aggiunto all'elenco. Selezionare l'ID applicazione di destinazione e fare clic su **impostare le credenziali**![as_powerpivot_refresh_sss_set_key](../media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key").  
  
11. Digitare l'ID utente Oracle e la Password Oracle e quindi fare clic su **OK**.  
  
 Per altre informazioni, vedere sezione "Per creare un'applicazione di destinazione per l'autenticazione di SQL Server" nella [Usa Secure Store con l'autenticazione di SQL Server (SharePoint Server 2013)](https://technet.microsoft.com/library/gg298949.aspx) (https://technet.microsoft.com/library/gg298949.aspx).  
  
## <a name="to-configure-the-powerpivot-service-application"></a>Per configurare l'applicazione di servizio PowerPivot  
  
1.  In Amministrazione centrale SharePoint fare clic su Gestisci applicazioni di servizio.  
  
2.  Fare clic sul nome dell'applicazione di servizio PowerPivot, ad esempio "Default applicazione del servizio PowerPivot".  
  
3.  Fare clic su **Configura impostazioni dell'applicazione di servizio** nella sezione Azioni.  
  
4.  Nel **Datarefresh** sezione, impostare il **PowerPivot dati Account di aggiornamento automatico**a`PowerPivotDataRefresh` e quindi fare clic su **OK**.  
  
     ![as_powerpivot_refresh_new_refresh_acount](../media/as-powerpivot-refresh-new-refresh-acount.gif "as_powerpivot_refresh_new_refresh_acount")  
  
## <a name="to-configure-the-workbook"></a>Per configurare la cartella di lavoro  
  
1.  Passare alla cartella di lavoro in raccolta PowerPivot e fare clic su **Gestisci aggiornamento dati**![as_powerpivot_refresh_manage_reresh](../media/as-powerpivot-refresh-manage-reresh.gif "as_powerpivot_refresh_manage_reresh").  
  
2.  Se viene visualizzata la pagina **Cronologia aggiornamento dati** , fare clic su **Configura pianificazione**.  
  
3.  Fare clic su **Abilita**.  
  
4.  Fare clic su **Aggiorna anche appena possibile**.  
  
5.  Nella sezione **Credenziali** fare clic su **Utilizza l'account di aggiornamento dati configurato dall'amministratore**.  
  
6.  Deselezionare **Tutte le origini dati**.  
  
7.  Selezionare **Aggiorna** per l'origine dati che utilizza i dati Oracle. Il nome dell'origine dati può essere modificato in Microsoft Excel nel menu **Dati**, **Connessioni**, **Proprietà** .  
  
8.  Nell'origine dati selezionare **Utilizza pianificazione predefinita**.  
  
9. Selezionare **Effettua la connessione utilizzando le credenziali salvate nel servizio di archiviazione sicura per accedere all'origine dati. Immettere l'ID usato per cercare le credenziali nella casella ID servizio di archiviazione sicura**.  
  
10. Nel **ID:** , digitare `OracleAuthentication`.  
  
11. Fare clic su **OK**.  
  
     Se viene visualizzato un messaggio di errore simile al seguente: `The provided Secure Store target application is either incorrectly configured or does not exist`.  
  
     Le due soluzioni comuni sono:  
  
    -   Verificare che l'ID applicazione di destinazione sia corretto.  
  
    -   Verificare di aver impostato le credenziali per l'applicazione di destinazione.  
  
## <a name="to-verify-data-refresh-with-the-new-authentication"></a>Per verificare l'aggiornamento dati con la nuova autenticazione  
 Quando si fa clic su **OK**, viene visualizzata la pagina **Cronologia aggiornamento** . Nell'arco di pochi minuti verrà visualizzato un nuovo elemento nella cronologia di aggiornamento perché nei passaggi precedenti è stato selezionato **Aggiorna anche appena possibile**. Il valore predefinito per il processo timer **Processo timer di aggiornamento dati PowerPivot** è di 1 minuto. Se non viene visualizzato un nuovo elemento nella cronologia di aggiornamento, attendere qualche minuto e aggiornare il browser. Se il nuovo elemento continua a non essere visualizzato, verificare il valore corrente del processo timer.  
  
## <a name="more-information"></a>Ulteriori informazioni  
  
-   [Configurare il servizio di archiviazione sicura in SharePoint 2013](https://technet.microsoft.com/library/ee806866.aspx).  
  
-   Vedere la sezione "Aggiornamento dati pianificato" di [aggiornamento dati PowerPivot con SharePoint 2013 e SQL Server 2012 SP1 (Analysis Services)](https://msdn.microsoft.com/library/jj879294.aspx#bkmk_windows_auth_interactive_data_refresh).  
  
  
