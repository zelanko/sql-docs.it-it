---
title: Creare ed eseguire il mapping di un ambiente Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isenvprop.variables.f1
- sql12.ssis.ssms.iscreateenv.f1
- sql12.ssis.ssms.isenvprop.permissions.f1
- sql12.ssis.ssms.isenvprop.general.f1
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d40f86706a8c2b9c3d8815398457073ca7acce0
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393269"
---
# <a name="create-and-map-a-server-environment"></a>Creare ed eseguire il mapping di un ambiente server
  Creare un ambiente server per specificare i valori di runtime per i pacchetti contenuti in un progetto distribuito nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. È quindi possibile eseguire il mapping delle variabili di ambiente ai parametri, per un pacchetto specifico, per i pacchetti del punto di ingresso o per tutti i pacchetti di un progetto specificato. Un pacchetto del punto di ingresso è in genere un pacchetto padre che esegue un pacchetto figlio.  
  
> [!IMPORTANT]  
>  Per un'esecuzione specifica, un pacchetto può essere eseguito solo con i valori contenuti in un ambiente server singolo.  
  
 È possibile eseguire query sulle viste per un elenco di ambienti server, riferimenti all'ambiente e variabili di ambiente. È inoltre possibile chiamare stored procedure per aggiungere, eliminare e modificare gli ambienti, i riferimenti all'ambiente e le variabili di ambiente. Per ulteriori informazioni, vedere la sezione **Ambienti server, variabili del server e riferimenti all'ambiente del server** in [SSIS Catalog](catalog/ssis-catalog.md).  
  
### <a name="to-create-and-use-a-server-environment"></a>Per creare e utilizzare un ambiente server  
  
1.  In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] espandere Cataloghi di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]> nodo **SSISDB** in Esplora oggetti e individuare la cartella **Ambienti** del progetto per il quale si vuole creare un ambiente.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Ambienti** e quindi scegliere **Creazione ambiente**.  
  
3.  Digitare un nome e una descrizione per l'ambiente, quindi fare clic su **OK**.  
  
4.  Fare clic con il pulsante destro del mouse sul nuovo ambiente e scegliere **Proprietà**.  
  
5.  Nella pagina **Variabili** effettuare le operazioni seguenti per aggiungere una variabile.  
  
    1.  Selezionare il **Tipo** per la variabile. Il nome della variabile **non deve** corrispondere al nome del parametro del progetto di cui verrà eseguito il mapping alla variabile.  
  
    2.  Immettere una **Descrizione** facoltativa per la variabile.  
  
    3.  Immettere il **Valore** per la variabile di ambiente.  
  
         Per informazioni sulle regole per i nomi delle variabili di ambiente, vedere la sezione **Variabile di ambiente** in [SSIS Catalog](catalog/ssis-catalog.md).  
  
    4.  Indicare se nella variabile è contenuto il valore sensibile, selezionando o deselezionando la casella di controllo **Sensibile** .  
  
         Se si seleziona **Sensibile**, il valore della variabile non viene visualizzato nel campo **Valore** .  
  
         I valori sensibili vengono crittografati nel catalogo SSISDB. Per ulteriori informazioni sulla crittografia, vedere [SSIS Catalog](catalog/ssis-catalog.md).  
  
6.  Nella pagina **Autorizzazioni** concedere o negare le autorizzazioni per gli utenti e i ruoli selezionati effettuando le operazioni riportate di seguito.  
  
    1.  Fare clic su **Sfoglia**, quindi selezionare uno o più utenti e ruoli nella finestra di dialogo **Sfoglia tutte le entità** .  
  
    2.  Nell'area **Account di accesso o ruoli** selezionare l'utente o il ruolo per cui si desidera concedere o negare le autorizzazioni.  
  
    3.  Nell'area **Esplicita** fare clic su **Concedi** o **Nega** accanto a ogni autorizzazione.  
  
7.  Per creare lo script dell'ambiente, fare clic su **Script**. Per impostazione predefinita, lo script viene visualizzato in una nuova finestra dell'editor di query.  
  
    > [!TIP]  
    >  È necessario fare clic su **Script** dopo aver apportato una o più modifiche alle proprietà dell'ambiente, ad esempio se si aggiunge una variabile, e prima di fare clic su **OK** nella finestra di dialogo **Proprietà ambiente**. In caso contrario, non viene creato alcuno script.  
  
8.  Fare clic su **OK** per salvare le modifiche apportate alle proprietà di ambiente.  
  
9. Nel nodo **SSISDB** in Esplora oggetti espandere la cartella **Progetti** , fare clic con il pulsante destro del mouse sul progetto e quindi fare clic su **Configura**.  
  
10. Nella pagina **Riferimenti** fare clic su **Aggiungi** per aggiungere un ambiente, quindi scegliere **OK** per salvare il riferimento all'ambiente.  
  
11. Fare nuovamente clic con il pulsante destro del mouse sul progetto e quindi scegliere **Configura**.  
  
12. Per eseguire il mapping della variabile di ambiente a un parametro aggiunto al pacchetto in fase di progettazione o a un parametro che è stato generato durante la conversione del progetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al modello di distribuzione del progetto, effettuare le operazioni seguenti.  
  
    1.  Nella scheda **Parametri** della pagina **Parametri** fare clic sul pulsante Sfoglia accanto al campo **Valore** .  
  
    2.  Fare clic su **Usa variabile di ambiente**, quindi selezionare la variabile di ambiente creata.  
  
13. Per eseguire il mapping della variabile di ambiente a una proprietà di gestione connessione, effettuare le operazioni seguenti. I parametri vengono automaticamente generati nel server SSIS per le proprietà di gestione connessione.  
  
    1.  Nella scheda **Gestioni connessioni** della pagina **Parametri** fare clic sul pulsante Sfoglia accanto al campo **Valore** .  
  
    2.  Fare clic su **Usa variabile di ambiente**, quindi selezionare la variabile di ambiente creata.  
  
14. Fare clic su **OK** due volte per salvare le modifiche.  
  
  
