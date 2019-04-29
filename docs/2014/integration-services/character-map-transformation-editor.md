---
title: Editor trasformazione mappa caratteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- Character Map Transformation Editor
ms.assetid: 3f1dbcf9-9cca-4606-bdcc-7ea6ad48cdf3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 847b05d76559cec2632b519a3b1cd3e0fbdb23ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62835134"
---
# <a name="character-map-transformation-editor"></a>Editor trasformazione Mappa caratteri
  Usare la finestra di dialogo **Editor trasformazione Mappa caratteri** per selezionare le funzioni per i valori stringa da applicare ai dati di colonna e per specificare se il mapping è una modifica sul posto o viene aggiunto come nuova colonna.  
  
 Per ulteriori informazioni sulla trasformazione Mappa caratteri, vedere [Character Map Transformation](data-flow/transformations/character-map-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Utilizzare le caselle di controllo per selezionare le colonne da trasformare utilizzando le funzioni per i valori stringa. Le selezioni verranno visualizzate nella tabella sottostante.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate nella tabella precedente. È inoltre possibile modificare o rimuovere una selezione utilizzando l'elenco di colonne di input disponibili.  
  
 **Destinazione**  
 Consente di specificare se salvare i risultati delle operazioni di stringa sul posto, utilizzando la colonna esistente, o se salvare i dati modificati come nuova colonna.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Nuova colonna|Consente di salvare i dati in una nuova colonna. Assegnare il nome alla colonna in **Alias di output**.|  
|Modifica sul posto|Consente di salvare i dati modificati nella colonna esistente.|  
  
 **Operazione**  
 Consente di selezionare nell'elenco le funzioni per i valori stringa da applicare ai dati della colonna.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Minuscolo|Consente di convertire la stringa in caratteri minuscoli.|  
|Maiuscolo|Consente di convertire la stringa in caratteri maiuscoli.|  
|Inversione byte|Consente di eseguire la conversione invertendo l'ordine dei byte.|  
|Hiragana|Consente di convertire i caratteri giapponesi katakana in caratteri hiragana.|  
|Katakana|Consente di convertire i caratteri giapponesi hiragana in caratteri katakana.|  
|Metà larghezza|Consente di convertire i caratteri a larghezza intera in caratteri a metà larghezza.|  
|Larghezza intera|Consente di convertire i caratteri a metà larghezza in caratteri a larghezza intera.|  
|Conversione da maiuscole a minuscole (e viceversa) basata sulla lingua|Consente di applicare le regole di conversione da maiuscole a minuscole (e viceversa) basata sulla lingua, ovvero il mapping Unicode semplice tra maiuscole e minuscole per il turco e altre impostazioni locali, al posto delle regole di sistema.|  
|Cinese semplificato|Consente di convertire i caratteri in cinese tradizionale in caratteri in cinese semplificato.|  
|Cinese tradizionale|Consente di convertire i caratteri in cinese semplificato in caratteri in cinese tradizionale.|  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. L'impostazione predefinita è **Copia di** seguita dal nome della colonna di input.  È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Configura output errori**  
 Usare la finestra di dialogo [Configura output errori](../../2014/integration-services/configure-error-output.md) per specificare le opzioni di gestione degli errori per la trasformazione corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
