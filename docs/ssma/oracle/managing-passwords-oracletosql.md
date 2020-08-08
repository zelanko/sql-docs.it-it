---
title: Gestione delle password (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/07/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Managing Passwords in Oracle, Exporting or Importing Encrypted Password
- Managing passwords in Oracle, Securing Password
ms.assetid: 8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: b96c7cff343c1c0f00c0e324961d633c4255f2a9
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934710"
---
# <a name="managing-passwords-oracletosql"></a>Gestione delle password (OracleToSQL)
In questa sezione viene illustrata la protezione delle password del database e la procedura per importarli o esportarli tra server.

## <a name="securing-password"></a>Sicurezza della password  
SSMA consente di proteggere la password di un database.  
  
Per implementare una connessione protetta, attenersi alla procedura seguente:  
  
Specificare una password valida utilizzando uno dei tre metodi seguenti:  
  
1.  **Testo non crittografato:** Digitare la password del database nell'attributo value del nodo ' password '. Si trova nel nodo definizione server della sezione server del file di script o di connessione al server.  
  
    Le password in testo non crittografato non sono sicure. Pertanto, nell'output della console verrà visualizzato il seguente messaggio di avviso: *"server &lt; -ID &gt; password è disponibile in formato testo non protetto, l'applicazione console SSMA fornisce un'opzione per proteggere la password tramite crittografia. per ulteriori informazioni, vedere l'opzione-SecurePassword nel file della Guida di SSMA."*  
  
    **Password crittografate:** La password specificata, in questo caso, viene archiviata in formato crittografato nel computer locale in ProtectedStorage. SSMA.  
  
    -   **Protezione delle password**  
  
        -   Eseguire `SSMAforOracleConsole.exe` con `-securepassword` e aggiungere switch alla riga di comando passando la connessione al server o il file di script contenente il nodo password nella sezione relativa alla definizione del server.  
  
        -   Al prompt, all'utente viene richiesto di immettere la password del database e di confermarla.  
  
            Gli ID di definizione del server e le password crittografate corrispondenti vengono archiviati in un file nel computer locale  
            
            Esempio 1:  
            
            1. Specificare la password
                
            2. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml"`
                
            3. Immettere la password per server_id ' XXX_1': xxxxxxx
                
            4. Immettere nuovamente la password per server_id ' XXX_1': xxxxxxx
            
            Esempio 2:
            
            1. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Oracle\Sample Console Scripts\ VariableValueFileSample.xml" -o`

            2. Immettere la password per server_id ' source_1': xxxxxxx

            3. Immettere nuovamente la password per server_id ' source_1': xxxxxxx

            4. Immettere la password per server_id ' target_1': xxxxxxx

            5. Immettere nuovamente la password per server_id ' destinazione _1': xxxxxxx  
    
    -   **Rimozione delle password crittografate**  
  
        Eseguire `SSMAforOracleConsole.exe` con l' `-securepassword` opzione e `-remove` nella riga di comando passando gli ID server per rimuovere le password crittografate dal file di archiviazione protetto presente nel computer locale.  
        
        Esempio:  

        ```console
        C:\SSMA\SSMAforOracleConsole.EXE -securepassword -remove all
        C:\SSMA\SSMAforOracleConsole.EXE -securepassword -remove "source_1,target_1"  
        ```

    -   **Elenco di ID server le cui password sono crittografate**  
  
        Eseguire `SSMAforOracleConsole.exe` con `-securepassword` e `-list` passare alla riga di comando per elencare tutti gli ID server le cui password sono state crittografate.  
  
        Esempio:  

        ```console
        C:\SSMA\SSMAforOracleConsole.EXE -securepassword -list  
        ```
  
    > [!NOTE]  
    > 1.  La password in testo non crittografato indicato nel file di connessione dello script o del server ha la precedenza sulla password crittografata in un file protetto.  
    > 2.  Se nella sezione server del file di connessione del server o del file di script non è presente alcuna password o se non è stata protetta nel computer locale, nella console viene richiesto di immettere la password.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Esportazione o importazione di password crittografate  
L'applicazione console SSMA consente di esportare le password di database crittografate presenti in un file nel computer locale in un file protetto e viceversa. Consente di rendere le password crittografate indipendenti dal computer. La funzionalità di esportazione consente di leggere l'ID e la password del server dall'archiviazione protetta locale e di salvare le informazioni in un file crittografato. All'utente viene richiesto di immettere la password per il file protetto. Verificare che la password immessa sia di 8 caratteri o superiore. Questo file protetto è portabile tra computer diversi. La funzionalità di importazione legge le informazioni relative all'ID server e alla password dal file protetto. All'utente viene richiesto di immettere la password per il file protetto e di accodare le informazioni all'archivio locale protetto.  
  
### <a name="export-example"></a>Esempio di esportazione:  

1. Esporta password

2. Immettere la password per la protezione del file esportato

3. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -export all "machine1passwords.file"`

4. Immettere la password per la protezione del file esportato: xxxxxxxx

5. Confermare la password: xxxxxxxx

6. `C:\SSMA\SSMAforOracleConsole.EXE -p -e "OracleDB_1_1,Sql_1" "machine2passwords.file"`

7. Immettere la password per la protezione del file esportato: xxxxxxxx

8. Confermare la password: xxxxxxxx  

### <a name="import-example"></a>Esempio di importazione:  

1. Importare una password crittografata

2. Immettere la password per la protezione del file importato

3. `C:\SSMA\SSMAforOracleConsole.EXE -securepassword -import all "machine1passwords.file"`

4. Immettere la password per importare i server dal file crittografato: xxxxxxxx

5. Confermare la password: xxxxxxxx

6. `C:\SSMA\SSMAforOracleConsole.EXE -p -i "OracleDB_1,Sql_1" "machine2passwords.file"`

7. Immettere la password per importare i server dal file crittografato: xxxxxxxx

8. Confermare la password: xxxxxxxx  

## <a name="see-also"></a>Vedere anche  
[Esecuzione della console SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
