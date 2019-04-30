---
title: La gestione delle password (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b099d0f9-dd37-4c87-8b6f-ed0177881ea4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bfa7b7481589ccb636147b3842a15b92f1a59d43
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63453694"
---
# <a name="managing-passwords-accesstosql"></a>La gestione delle password (AccessToSQL)
Questa sezione riguarda la protezione delle password di database e la procedura per importare o esportare tali tra server:  
  
1.  Protezione di Password  
  
2.  L'esportazione o importazione di Password crittografata  
  
## <a name="securing-password"></a>Protezione di Password  
SSMA consente di proteggere la password di un database.  
  
Usare la procedura seguente per implementare una connessione sicura:  
  
Specificare una password valida usando uno dei tre metodi seguenti:  
  
1.  **Testo non crittografato:** Digitare la password del database nell'attributo valore del nodo 'password'. Si trova sotto il nodo della definizione di server nella sezione Server di file di script o file di connessione server.  
  
    Le password in testo non crittografato non sono protette. Pertanto, si verificherà il seguente messaggio di avviso nell'output della console: *"Server &lt;server-id&gt; password viene fornita in formato testo non crittografato non sicure, applicazione Console SSMA fornisce un'opzione per proteggere la password mediante crittografia, vedere securepassword - opzione nel file della Guida SSMA per altre informazioni informazioni".*  
  
    **Password crittografate:** La password specificata, in questo caso, viene archiviata in formato crittografato nel computer locale in ProtectedStorage.ssma.  
  
    -   **Protezione delle password**  
  
        -   Eseguire la `SSMAforAccessConsole.exe` con il `-securepassword` e aggiunge l'opzione nella riga di comando passando il server di connessione o file script che contiene il nodo della password nella sezione Definizione server.  
  
        -   Al prompt dei comandi, l'utente viene richiesto di immettere la password del database e confermarla.  
  
            Gli ID definizione di server e relativa password crittografata corrispondenti vengono archiviate in un file nel computer locale  
  
            Esempio 1:
            
                Specify password
                
                C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx  
            
            Esempio 2:
            
                C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
  
    -   **Rimozione delle password crittografate**  
  
        Eseguire la `SSMAforAccessConsole.exe` con il`-securepassword` e `-remove` passare alla riga di comando passando l'ID server, per rimuovere le password crittografate dal file di archiviazione protetto presentano nel computer locale.  
  
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove all
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove "source_1,target_1"  
  
    -   **Elenco di ID Server le cui password vengono crittografate**  
  
        Eseguire il SSMAforAccessConsole.exe con il `-securepassword` e `-list` passare alla riga di comando per elencare tutti gli ID server le cui password sono state crittografate.  
  
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -list  
  
    > [!NOTE]  
    > 1.  La password in testo non crittografato indicato nel file di connessione di server o lo script ha la precedenza sulla password crittografata nel file protetto.  
    > 2.  Quando è presente alcuna password nella sezione server di file di connessione del server o il file di script o se non è stato protetto nel computer locale, la console viene richiesto di immettere la password.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Esportare o importare le password crittografate  
L'applicazione Console SSMA consente di esportare le password crittografate del database presente in un file nel computer locale in un file protetto e viceversa. È utile nella creazione della macchina password crittografate indipendenti. La funzionalità di esportazione legge l'id del server e protetto da archiviazione di password da locale e Salva le informazioni in un file crittografato. L'utente viene richiesto di immettere la password per il file protetto. Assicurarsi che la password immessa è 8 caratteri o più. Questo file protetto sia portabile tra computer diversi. Funzionalità di importazione legge il server di informazioni su id e la password dal file protetto. L'utente viene richiesto di immettere la password per il file protetto e aggiunge le informazioni nell'archiviazione locale protetto.  


    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforAccessConsole.EXE -securepassword -export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE -p -e "AccessDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  


    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforAccessConsole.EXE -securepassword -import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE -p -i "AccessDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della Console SSMA (accesso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
