---
layout: HubPage
hide_bc: true
title: Progettazione di database di SQL Server
description: Informazioni sulle funzionalità di SQL Server che consentono di progettare il database più adatto alle proprie esigenze aziendali.
ms.topic: hub-page
ms.prod: sql
author: MashaMSFT
ms.author: mathoma
ms.date: 12/15/2018
featureFlags:
- clicktale
ms.openlocfilehash: c08b067a8c92b7fea32b53cd8b14b7ecc13272d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077237"
---
<div id="main" class="v2">
    <div class="container">
        <ul class="cardsY panelContent featuredContent">
            <li>
                <a href="https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-ctp">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-sql-server.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Provare SQL Server 2019 (anteprima)</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/get-azure-sql-vm.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Ottenere una macchina virtuale con SQL Server</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="/sql/ssms/download-sql-server-management-studio-ssms">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-ssms.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Scaricare SQL Server Management Studio</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>              
        </ul>
    </div>
    <div class="container">
        <h1>SQL Server: Progettazione di database</h1>
        <ul class="pivots tabLess">
            <li class="pivotItem" style="display: list-item;" data-id="#products">
                <a href="#products" data-linktype="self-bookmark"></a>
                <ul id="products">
                    <li class="panelItem" data-index="0">
                        <a class="singlePanelNavItem selected" href="#products1" data-linktype="self-bookmark"></a>
                        <ul class="cardsD panelContent singlePanelContent" id="products1" style="margin-top: 0px; display: flex;">
                            <li>
                                <a href="/sql/relational-databases/collations/collation-and-unicode-support/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/collation.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Regole di confronto</h3>
                                                    <p>Le regole di confronto in SQL Server offrono regole di ordinamento e proprietà di distinzione tra maiuscole e minuscole e tra caratteri accentati e non accentati per i dati. Le regole di confronto utilizzate con dati di tipo carattere, quali char e varchar, definiscono la tabella codici e i caratteri corrispondenti che possono essere rappresentati per quel tipo di dati. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/databases/databases/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/databases.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Database</h3>
                                                    <p>Un database in SQL Server è costituito da una raccolta di tabelle in cui è archiviato un set specifico di dati strutturati. Una tabella contiene una raccolta di righe, definite anche record o tuple, e colonne, definite anche attributi.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> <li>
                                <a href="/sql/relational-databases/blob/filestream-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/filestream.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Filestream</h3>
                                                    <p>FileStream consente alle applicazioni basate su SQL Server di archiviare nel file system dati non strutturati, ad esempio documenti e immagini.  </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/blob/filetables-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/filetable.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>FileTable</h3>
                                                    <p>FileTable consente l'integrazione dei componenti di archiviazione e gestione dei dati da parte di un'applicazione e fornisce servizi di SQL Server integrati, incluse la ricerca full-text e la ricerca semantica, su dati e metadati non strutturati.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/graphs/sql-graph-overview/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/sql-graphs.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Grafico</h3>
                                                    <p>Un database a grafo è una raccolta di nodi (o vertici) e archi (o relazioni). Un nodo rappresenta un'entità (ad esempio, una persona o un'organizzazione) e un arco rappresenta una relazione tra i due nodi che connette (ad esempio, Mi piace o amici). </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/hierarchical-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/hierarchy-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Dati gerarchici</h3>
                                                    <p>I dati gerarchici vengono definiti come un set di elementi di dati correlati tra loro tramite relazioni gerarchiche. Si parla di relazioni gerarchiche quando un elemento di dati è l'elemento padre di un altro elemento.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/indexes/indexes/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/indexes.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Indici</h3>
                                                    <p>Panoramica dei diversi tipi di indici usati da SQL per organizzare i dati. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/sequence-numbers/sequence-numbers/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/sequence-numbers.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Numeri di sequenza</h3>
                                                    <p>Una sequenza è un oggetto associato a schema definito dall'utente che genera una sequenza di valori numerici in base alla specifica con la quale è stata creata la sequenza.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/spatial/spatial-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/spatial-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Dati spaziali</h3>
                                                    <p>I dati spaziali rappresentano informazioni sulla posizione fisica e sulla forma di oggetti geometrici. Questi oggetti possono essere posizioni dei punti oppure oggetti più complessi ad esempio paesi, strade o laghi. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/stored-procedures/stored-procedures-database-engine/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/stored-procedures.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Stored procedure</h3>
                                                    <p>Una stored procedure in SQL Server è un gruppo di una o più istruzioni Transact-SQL oppure un riferimento a un metodo CLR (Common Runtime Language) di Microsoft .NET Framework. Le stored procedure assomigliano ai costrutti di altri linguaggi di programmazione.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/tables/tables/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/tables.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Tabelle</h3>
                                                    <p>Le tabelle sono oggetti di database che contengono tutti i dati presenti in un database. Nelle tabelle, i dati sono organizzati in modo logico in righe e colonne in un formato simile a quello di un foglio di calcolo. Ogni riga rappresenta un record univoco e ogni colonna rappresenta un campo all'interno del record.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/track-changes/track-data-changes-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/track-changes.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Rilevamento modifiche</h3>
                                                    <p>Panoramica di due funzionalità che consentono di tenere traccia delle modifiche ai dati: Change Data Capture e rilevamento modifiche.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/triggers/logon-triggers/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/triggers.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Trigger</h3>
                                                    <p>I trigger consentono una risposta automatica a un'azione specifica, ad esempio l'accesso o un comando ALTER DATABASE. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/views/views/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/views.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Viste</h3>
                                                    <p>Una vista è una tabella virtuale il cui contenuto è definito da una query.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>  
                            <li>
                                <a href="/sql/relational-databases/xml/xml-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/xml-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>dati XML</h3>
                                                    <p>Panoramica delle potenzialità del tipo di dati XML, degli indici XML, delle raccolte di schemi XML e altro ancora. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                                    <li>
                                      <a href="/sql/lp/sql-server/query-data/">
                                          <div class="cardSize">
                                              <div class="cardPadding">
                                                  <div class="card">
                                                      <div class="cardImageOuter">
                                                          <div class="cardImage">
                                                              <img src="media/index/query-data.svg" alt="" /> 
                                                          </div>
                                                      </div>
                                                      <div class="cardText">
                                                          <h3>Eseguire query sui dati</h3>
                                                          <p><b>Cursori, sinonimi, scripting, join, funzioni definite dall'utente, ricerca full-text </b></p>
                                                      </div>
                                                  </div>
                                              </div>
                                          </div>
                                      </a>
                                    </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</div>
<div class="container centered pageFooter">
        <h2>Rimani in contatto con noi</h2>
        <ul class="links">
           <li>
                <a href="https://aka.ms/editsqldocs" data-linktype="external"> Collaborazione </a>
            </li>
           <li>
                <a href="https://docs.microsoft.com/sql/sql-server/sql-server-get-help" data-linktype="external"> Supporto </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsfeedback" data-linktype="external"> Commenti e suggerimenti </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsurvey" data-linktype="external"> Sondaggio </a>
            </li>
           <li>
                <a href="https://cloudblogs.microsoft.com/sqlserver/" data-linktype="external"> Blog </a>
            </li>
            <li>
                <a href="https://twitter.com/sqldocs" data-linktype="external"> Twitter </a>
            </li>
            <li>
                <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqldatabaseengine&filter=alltypes&sort=lastpostdesc" data-linktype="external"> Forum di MSDN </a>
            </li>
            <li>
                <a href="https://feedback.azure.com/forums/908035-sql-server" data-linktype="external"> User Voice </a>
            </li>
        </ul>
    </div>