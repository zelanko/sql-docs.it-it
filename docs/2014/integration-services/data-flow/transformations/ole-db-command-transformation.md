---
title: Trasformazione Comando OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3a8ffc33de161c71c6f72eebf8616d1e814fb994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770390"
---
# <a name="ole-db-command-transformation"></a>Comando OLE DB - trasformazione
  La trasformazione Comando OLE DB esegue un'istruzione SQL per ogni riga in un flusso di dati. È ad esempio possibile eseguire un'istruzione SQL che inserisce, aggiorna o elimina righe in una tabella di database.  
  
 Per configurare la trasformazione comando OLE DB, procedere nel modo seguente:  
  
-   Specificare l'istruzione SQL eseguita dalla trasformazione per ogni riga.  
  
-   Specificare il numero di secondi prima del timeout dell'istruzione SQL.  
  
-   Specificare la tabella codici predefinita.  
  
 In genere l'istruzione SQL include parametri. I valori dei parametri vengono archiviati in colonne esterne nell'input della trasformazione e, se si esegue il mapping di una colonna di input a una colonna esterna, verrà eseguito il mapping di una colonna di input a un parametro. Per individuare ad esempio le righe della tabella **DimProduct** in base al valore nella relativa colonna **ProductKey** ed eliminarle, è possibile eseguire il mapping della colonna esterna con il nome **Param_0** alla colonna di input con il nome **ProductKey,** , quindi eseguire l'istruzione SQL `DELETE FROM DimProduct WHERE ProductKey = ?`. I nomi dei parametri sono specificati dalla trasformazione Comando OLE DB e non possono essere modificati. I nomi dei parametri sono **Param_0**, **Param_1**e così via.  
  
 Se si configura la trasformazione Comando OLE DB tramite la finestra di dialogo **Editor avanzato** , sarà possibile eseguire automaticamente il mapping dei parametri dell'istruzione SQL alle colonne esterne nell'input della trasformazione e definire le caratteristiche di ogni parametro facendo clic sul pulsante **Aggiorna** . Se tuttavia il provider OLE DB utilizzato dalla trasformazione Comando OLE DB non supporta la derivazione di informazioni sui parametri dai parametri, sarà necessario configurare le colonne esterne manualmente. Questo significa che è necessario aggiungere una colonna per ogni parametro all'input esterno della trasformazione, aggiornare i nomi delle colonne in modo da usare nomi quale **Param_0**, specificare il valore della proprietà DBParamInfoFlags ed eseguire il mapping delle colonne di input contenenti i valori dei parametri alle colonne esterne.  
  
 Il valore di DBParamInfoFlags rappresenta le caratteristiche del parametro. Il valore **1** , ad esempio, specifica che si tratta di un parametro di input, mentre il valore **65** specifica che si tratta di un parametro di input che può contenere un valore Null. I valori devono corrispondere a quelli nell'enumerazione OLE DB DBPARAMFLAGSENUM. Per ulteriori informazioni, vedere la documentazione di riferimento di OLE DB.  
  
 La trasformazione Comando OLE DB include la proprietà personalizzata `SQLCommand`, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
 Questa trasformazione include un input, un output regolare e un output degli errori.  
  
## <a name="logging"></a>Registrazione  
 È possibile registrare le chiamate eseguite dalla trasformazione Comando OLE DB a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni e ai comandi a origini dati esterne impartiti dalla trasformazione Comando OLE DB. Per registrare le chiamate eseguite dalla trasformazione Comando OLE DB a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile configurare la trasformazione utilizzando Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o il modello a oggetti. Per informazioni dettagliate sulla configurazione della trasformazione usando Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , vedere  [Configurazione della trasformazione Comando OLE DB](../../configure-the-ole-db-command-transformation.md). Vedere la Guida per gli sviluppatori per informazioni dettagliate sulla configurazione a livello di codice di questa trasformazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
