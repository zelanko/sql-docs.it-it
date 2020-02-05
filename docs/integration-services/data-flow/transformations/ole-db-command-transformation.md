---
title: Trasformazione Comando OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09850707b83481909a881dcefdf00e710e6a8790
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71291240"
---
# <a name="ole-db-command-transformation"></a>Comando OLE DB - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Comando OLE DB esegue un'istruzione SQL per ogni riga in un flusso di dati. È ad esempio possibile eseguire un'istruzione SQL che inserisce, aggiorna o elimina righe in una tabella di database.  
  
 Per configurare la trasformazione comando OLE DB, procedere nel modo seguente:  
  
-   Specificare l'istruzione SQL eseguita dalla trasformazione per ogni riga.  
  
-   Specificare il numero di secondi prima del timeout dell'istruzione SQL.  
  
-   Specificare la tabella codici predefinita.  
  
 In genere l'istruzione SQL include parametri. I valori dei parametri vengono archiviati in colonne esterne nell'input della trasformazione e, se si esegue il mapping di una colonna di input a una colonna esterna, verrà eseguito il mapping di una colonna di input a un parametro. Per individuare ad esempio le righe della tabella **DimProduct** in base al valore nella relativa colonna **ProductKey** ed eliminarle, è possibile eseguire il mapping della colonna esterna con il nome **Param_0** alla colonna di input con il nome **ProductKey,** , quindi eseguire l'istruzione SQL `DELETE FROM DimProduct WHERE ProductKey = ?`. I nomi dei parametri sono specificati dalla trasformazione Comando OLE DB e non possono essere modificati. I nomi dei parametri sono **Param_0**, **Param_1**e così via.  
  
 Se si configura la trasformazione Comando OLE DB tramite la finestra di dialogo **Editor avanzato** , sarà possibile eseguire automaticamente il mapping dei parametri dell'istruzione SQL alle colonne esterne nell'input della trasformazione e definire le caratteristiche di ogni parametro facendo clic sul pulsante **Aggiorna** . Se tuttavia il provider OLE DB utilizzato dalla trasformazione Comando OLE DB non supporta la derivazione di informazioni sui parametri dai parametri, sarà necessario configurare le colonne esterne manualmente. Questo significa che è necessario aggiungere una colonna per ogni parametro all'input esterno della trasformazione, aggiornare i nomi delle colonne in modo da usare nomi quale **Param_0**, specificare il valore della proprietà DBParamInfoFlags ed eseguire il mapping delle colonne di input contenenti i valori dei parametri alle colonne esterne.  
  
 Il valore di DBParamInfoFlags rappresenta le caratteristiche del parametro. Il valore **1** , ad esempio, specifica che si tratta di un parametro di input, mentre il valore **65** specifica che si tratta di un parametro di input che può contenere un valore Null. I valori devono corrispondere a quelli nell'enumerazione OLE DB DBPARAMFLAGSENUM. Per ulteriori informazioni, vedere la documentazione di riferimento di OLE DB.  
  
 La trasformazione Comando OLE DB include la proprietà personalizzata **SQLCommand** , che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Questa trasformazione include un input, un output regolare e un output degli errori.  
  
## <a name="logging"></a>Registrazione  
 È possibile registrare le chiamate eseguite dalla trasformazione Comando OLE DB a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni e ai comandi a origini dati esterne impartiti dalla trasformazione Comando OLE DB. Per registrare le chiamate eseguite dalla trasformazione Comando OLE DB a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile configurare la trasformazione utilizzando Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o il modello a oggetti. Vedere la Guida per gli sviluppatori per informazioni dettagliate sulla configurazione a livello di codice di questa trasformazione.  
  
## <a name="configure-the-ole-db-command-transformation"></a>Configurazione della trasformazione Comando OLE DB
  È possibile aggiungere e configurare una trasformazione Comando OLE DB solo se il pacchetto include almeno un'attività Flusso di dati e un'origine, quale un'origine file flat o un'origine OLE DB. Questa trasformazione viene in genere utilizzata per l'esecuzione di query con parametri.  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>Per configurare la trasformazione Comando OLE DB  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**trascinare la trasformazione Comando OLE DB sull'area di progettazione.  
  
4.  Connettere la trasformazione Comando OLE DB al flusso di dati trascinando un connettore, la freccia verde o la freccia rossa, da un'origine dei dati o una trasformazione precedente alla trasformazione Comando OLE DB.  
  
5.  Fare clic con il pulsante destro del mouse sul componente e scegliere Modifica o **Visualizza editor avanzato**.  
  
6.  Nella scheda **Gestioni connessioni** selezionare una gestione connessione OLE DB dall'elenco **Gestione connessione** . Per altre informazioni, vedere [Gestione connessione OLE DB](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Fare clic sulla scheda **Proprietà componente** e quindi sul pulsante con i puntini di sospensione **(...)** nella casella **SqlCommand** .  
  
8.  In **Editor valore stringa**digitare l'istruzione SQL con parametri usando un punto interrogativo (?) come indicatore per ogni parametro.  
  
9. Fare clic su **Aggiorna**. Quando si fa clic su **Aggiorna**la trasformazione crea una colonna per ogni parametro nella raccolta Colonne esterne e imposta la proprietà DBParamInfoFlags.  
  
10. Fare clic sulla scheda **Proprietà input e output** .  
  
11. Espandere **Input comando OLE DB**e quindi **Colonne esterne**.  
  
12. Verificare che in **Colonne esterne** sia elencata una colonna per ogni parametro nell'istruzione SQL. I nomi delle colonne sono **Param_0**, **Param_1**e così via.  
  
     Tali nomi non devono essere modificati. Se si modificano i nomi della colonna, [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] genera un errore di convalida per la trasformazione Comando OLE DB.  
  
     Inoltre, non modificare il tipo di dati. La proprietà DataType di ogni colonna viene impostata sul tipo di dati corretto.  
  
13. Se in **Colonne esterne** non è elencata alcuna colonna, sarà necessario aggiungerle manualmente.  
  
    -   Fare clic su **Aggiungi colonna** una volta per ogni parametro nell'istruzione SQL.  
  
    -   Modificare i nomi delle colonne in **Param_0**, **Param_1**e così via.  
  
    -   Specificare un valore nella proprietà DBParamInfoFlags. Tale valore deve corrispondere a un valore dell'enumerazione OLE DB DBPARAMFLAGSENUM. Per ulteriori informazioni, vedere la documentazione di riferimento di OLE DB.  
  
    -   Specificare il tipo di dati della colonna e, a seconda del tipo di dati, specificarne anche la tabella codici, la lunghezza, la precisione e la scala.  
  
    -   Per eliminare un parametro non usato, selezionarlo in **Colonne esterne**e fare clic su **Rimuovi colonna**.  
  
    -   Fare clic su **Mapping colonne** ed eseguire il mapping delle colonne nell'elenco **Colonne di input disponibili** ai parametri nell'elenco **Colonne di destinazione disponibili** .  
  
14. Fare clic su **OK**.  
  
15. Per salvare il pacchetto aggiornato, scegliere **Salva** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
