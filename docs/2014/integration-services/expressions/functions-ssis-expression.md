---
title: Funzioni (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9a3b62c843508d100623549097b670487dd16641
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801933"
---
# <a name="functions-ssis-expression"></a>Funzioni (espressione SSIS)
  Nel linguaggio delle espressioni è incluso un set di funzioni che è possibile utilizzare nelle espressioni. Un'espressione può contenere anche una sola funzione, ma in genere in un'espressione vengono utilizzate più funzioni, in combinazione con vari operatori.  
  
 Le funzioni disponibili possono essere suddivise nelle categorie seguenti:  
  
-   Funzioni matematiche. Eseguono calcoli basati su valori di input numerici specificati come parametri e restituiscono valori numerici.  
  
-   Funzioni per i valori stringa. Eseguono operazioni su valori di input di tipo stringa o esadecimale e restituiscono un valore stringa o numerico.  
  
-   Funzioni di data e ora. Eseguono operazioni su valori di data e ora e restituiscono valori stringa, numerici o di data e ora.  
  
-   Funzioni di sistema. Restituiscono informazioni relative a un'espressione.  
  
 Il linguaggio delle espressioni include le funzioni matematiche seguenti.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[ABS &#40;espressione SSIS&#41;](abs-ssis-expression.md)|Restituisce il valore positivo assoluto di un'espressione numerica.|  
|[EXP &#40;espressione SSIS&#41;](exp-ssis-expression.md)|Restituisce il valore della base e elevato all'espressione specificata.|  
|[CEILING &#40;espressione SSIS&#41;](ceiling-ssis-expression.md)|Restituisce il più piccolo valore integer maggiore o uguale a un'espressione numerica specificata.|  
|[FLOOR &#40;espressione SSIS&#41;](floor-ssis-expression.md)|Restituisce il più alto valore integer minore o uguale a un'espressione numerica specificata.|  
|[LN &#40;espressione SSIS&#41;](ln-ssis-expression.md)|Restituisce il logaritmo naturale di un'espressione numerica.|  
|[LOG &#40;espressione SSIS&#41;](log-ssis-expression.md)|Viene restituito il logaritmo in base 10 di un'espressione numerica.|  
|[POWER &#40;espressione SSIS&#41;](power-ssis-expression.md)|Restituisce il risultato dell'elevamento a potenza di un'espressione numerica.|  
|[ROUND &#40;espressione SSIS&#41;](round-ssis-expression.md)|Restituisce un'espressione numerica arrotondata alla lunghezza o alla precisione specificata. .|  
|[SIGN &#40;espressione SSIS&#41;](sign-ssis-expression.md)|Restituisce il segno positivo (+), negativo (-) o zero (0) di un'espressione numerica.|  
|[SQUARE &#40;espressione SSIS&#41;](square-ssis-expression.md)|Restituisce il quadrato di un'espressione numerica.|  
|[SQRT &#40;espressione SSIS&#41;](sqrt-ssis-expression.md)|Restituisce la radice quadrata di un'espressione numerica.|  
  
 L'analizzatore di espressioni include le funzioni per i valori stringa seguenti.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[CODEPOINT &#40;espressione SSIS&#41;](codepoint-ssis-expression.md)|Restituisce il codice Unicode corrispondente al primo carattere a sinistra in una stringa di caratteri.|  
|[FINDSTRING &#40;espressione SSIS&#41;](findstring-ssis-expression.md)|Restituisce l'indice in base uno dell'occorrenza specificata di una determinata stringa di caratteri in un'espressione.|  
|[HEX &#40;espressione SSIS&#41;](hex-ssis-expression.md)|Viene restituita una stringa che rappresenta il valore esadecimale di un valore integer.|  
|[LEN &#40;espressione SSIS&#41;](len-ssis-expression.md)|Viene restituito il numero di caratteri in un'espressione di caratteri.|  
|[LEFT &#40;espressione SSIS&#41;](left-ssis-expression.md)|Viene restituito il numero specificato di caratteri della parte più a sinistra dell'espressione di caratteri indicata.|  
|[LOWER &#40;espressione SSIS&#41;](lower-ssis-expression.md)|Viene restituita un'espressione di caratteri dopo aver convertito i caratteri maiuscoli in caratteri minuscoli.|  
|[LTRIM &#40;espressione SSIS&#41;](trim-ssis-expression.md)|Restituisce un'espressione di caratteri dopo aver rimosso gli spazi iniziali.|  
|[REPLACE &#40;espressione SSIS&#41;](replace-ssis-expression.md)|Restituisce un'espressione di caratteri dopo aver sostituito una stringa nell'espressione con un'altra stringa o una stringa vuota.|  
|[REPLICATE &#40;espressione SSIS&#41;](replicate-ssis-expression.md)|Viene restituita un'espressione di caratteri ripetuta per il numero di volte specificato.|  
|[REVERSE &#40;espressione SSIS&#41;](reverse-ssis-expression.md)|Viene restituita un'espressione di caratteri in ordine inverso.|  
|[RIGHT &#40;espressione SSIS&#41;](right-ssis-expression.md)|Viene restituito il numero specificato di caratteri della parte più a destra dell'espressione di caratteri indicata.|  
|[RTRIM &#40;espressione SSIS&#41;](rtrim-ssis-expression.md)|Viene restituita un'espressione di caratteri dopo aver rimosso gli spazi finali.|  
|[SUBSTRING &#40;espressione SSIS&#41;](substring-ssis-expression.md)|Restituisce parte di un'espressione di caratteri.|  
|[TRIM &#40;espressione SSIS&#41;](trim-ssis-expression.md)|Restituisce un'espressione di caratteri dopo aver rimosso gli spazi iniziali e finali.|  
|[UPPER &#40;espressione SSIS&#41;](upper-ssis-expression.md)|Restituisce un'espressione di caratteri dopo aver convertito i caratteri minuscoli in caratteri maiuscoli.|  
  
 L'analizzatore di espressioni fornisce le funzioni di data e ora seguenti.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[DATEADD &#40;espressione SSIS&#41;](dateadd-ssis-expression.md)|Restituisce un nuovo valore DT_DBTIMESTAMP ottenuto aggiungendo una data o un intervallo di tempo a una data specificata.|  
|[DATEDIFF &#40;espressione SSIS&#41;](datediff-ssis-expression.md)|Restituisce il numero di unità di data e ora trascorse tra due date specificate.|  
|[DATEPART &#40;espressione SSIS&#41;](datepart-ssis-expression.md)|Restituisce un valore integer che rappresenta una parte di una data.|  
|[DAY &#40;espressione SSIS&#41;](day-ssis-expression.md)|Restituisce un valore integer che rappresenta il giorno nella data specificata.|  
|[GETDATE &#40;espressione SSIS&#41;](getdate-ssis-expression.md)|Restituisce la data di sistema corrente.|  
|[GETUTCDATE &#40;espressione SSIS&#41;](getutcdate-ssis-expression.md)|Restituisce la data corrente del sistema in base all'ora UTC (Universal Time Coordinate o ora di Greenwich).|  
|[MONTH &#40;espressione SSIS&#41;](month-ssis-expression.md)|Restituisce un valore integer che rappresenta il mese nella data specificata.|  
|[YEAR &#40;espressione SSIS&#41;](year-ssis-expression.md)|Restituisce un valore integer che rappresenta l'anno nella data specificata.|  
  
 L'analizzatore di espressioni include le funzioni Null seguenti.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[ISNULL &#40;espressione SSIS&#41;](null-ssis-expression.md)|Restituisce un risultato booleano che varia a seconda che un'espressione abbia o meno un valore Null.|  
|[NULL &#40;espressione SSIS&#41;](null-ssis-expression.md)|Restituisce un valore Null di un tipo di dati richiesto.|  
  
 I nomi delle espressioni sono indicati in maiuscolo, ma non viene fatta distinzione tra maiuscole e minuscole. È ad esempio possibile utilizzare indifferentemente "null" o "NULL".  
  
## <a name="see-also"></a>Vedere anche  
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)   
 [Esempi di espressioni avanzate di Integration Services](examples-of-advanced-integration-services-expressions.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md)  
  
  
