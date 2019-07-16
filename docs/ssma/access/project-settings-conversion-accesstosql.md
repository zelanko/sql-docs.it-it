---
title: Impostazioni (conversione) (AccessToSQL) del progetto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- conversion, options described
- Project Settings dialog box, Conversion
ms.assetid: bcebc635-c638-4ddb-924c-b9ccfef86388
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ff44d34e6c701c8d43260982d3117def4cb9530d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929450"
---
# <a name="project-settings-conversion-accesstosql"></a>Impostazioni progetto (conversione) (AccessToSQL)
Le impostazioni del progetto di conversione consentono di configurare come gli oggetti vengono convertiti da oggetti di database di Access da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o oggetti di database di SQL Azure.  
  
Nel riquadro di conversione è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo.  
  
-   Usare la **impostazioni del progetto** finestra di dialogo per impostare le opzioni di configurazione per il progetto corrente. Per accedere a impostazioni di conversione, scegliere il **strumenti** dal menu **le impostazioni del progetto**, fare clic su **generale** nella parte inferiore del riquadro a sinistra e quindi selezionare  **Conversione**.  
  
-   Usare la **impostazioni di progetto predefinite** finestra di dialogo per impostare le opzioni di configurazione per tutti i progetti. Per accedere a impostazioni di conversione, scegliere il **strumenti** dal menu **impostazioni di progetto predefinite**, selezionare tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati / modificato da  **Versione di destinazione della migrazione** elenco a discesa, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi selezionare **conversione**.  
  
## <a name="options"></a>Opzioni  
**Aggiungere la chiave primaria**  
Crea una nuova chiave primaria nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o se una tabella di Access non ha alcuna chiave primaria o un indice univoco nella tabella di SQL Azure.  
  
-   **Modalità predefinita**: False  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
Quando si è connessi a SQL Azure, è per impostazione predefinita True. **Aggiungere colonne timestamp**  
Specifica se SSMA deve creare un valore di timestamp, se necessario.  
  
-   **Modalità predefinita**: Dipendente SSMA  
  
-   **La modalità ottimistico**: Never  
  
-   **Modalità intero**: Dipendente SSMA  
  
**Includere un report di valutazione dei dati con report di valutazione di conversione**  
Include una valutazione dei dati del report di valutazione.  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
**Tipo di messaggio quando una chiave primaria include le colonne nullable**  
Specifica il tipo di messaggio (avviso, errore o nulla) che mostra SSMA nel riquadro di Output quando rileva le chiavi primarie con le colonne nullable.  
  
-   **Modalità predefinita**: Avviso  
  
-   **La modalità ottimistico**: Nessun messaggio  
  
-   **Modalità intero**: Errore  
  
**Tipo di messaggio quando le colonne chiave esterna sono di dimensioni diverse**  
Specifica il tipo di messaggio (avviso, errore o nulla) che mostra SSMA nel riquadro di Output quando viene trovata una chiave esterna di testo non corretta.  
  
-   **Modalità predefinita**: Avviso  
  
-   **La modalità ottimistico**: Nessun messaggio  
  
-   **Modalità intero**: Errore  
  
**Tipo di messaggio quando le colonne di tipo memo siano indicizzate**  
Specifica il tipo di messaggio (avviso, errore o nulla) che mostra SSMA nel riquadro di Output quando rileva un indice che contiene un **memo** colonna.  
  
-   **Modalità predefinita**: Avviso  
  
-   **La modalità ottimistico**: Nessun messaggio  
  
-   **Modalità intero**: Errore  
  
**Avvisa quando una query complessa viene usato un carattere jolly (\&#42;)**  
Quando viene visualizzato un avviso nel riquadro di Output ed elenco errori un nome di colonna in un'istruzione SELECT è un carattere jolly (*).  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
**Avvisa quando viene modificato il nome di identificatore**  
Visualizza un messaggio nel rapporto di valutazione e nel riquadro di Output quando viene modificato un nome di identificatore di oggetto da SSMA.  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
**Avvisa quando identificatore racchiuso tra virgolette**  
Visualizza un messaggio nel rapporto di valutazione e nel riquadro di Output quando il nome di un identificatore di oggetto verrà racchiusi SSMA. Deve essere racchiuso tra gli identificatori è necessario quando il nome è una parola chiave o contiene caratteri speciali.  
  
-   **Modalità predefinita**: True  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
## <a name="see-also"></a>Vedere anche  
[Reference(Access) dell'interfaccia utente](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
