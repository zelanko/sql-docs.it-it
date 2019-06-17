---
title: API di estendibilità
titleSuffix: Azure Data Studio
description: Informazioni sulle API di estensibilità per Data Studio di Azure
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 3cde890f16e14866238f24e5d8a6bd52efdc9ecc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782414"
---
# <a name="azure-data-studio-extensibility-apis"></a>API di estendibilità Data Studio Azure

[!INCLUDE[name-sos](../includes/name-sos.md)] fornisce un'API che le estensioni possono usare per interagire con altre parti di Studio di dati di Azure, ad esempio Esplora oggetti. Queste API sono disponibili i [ `src/sql/sqlops.d.ts` ](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.d.ts) file e sono descritti di seguito.

## <a name="connection-management"></a>Gestione delle connessioni
`sqlops.connection`

### <a name="top-level-functions"></a>Funzioni di primo livello

- `getCurrentConnection(): Thenable<sqlops.connection.Connection>` Ottiene la connessione corrente in base all'editor attivo o selezione di Esplora oggetti.

- `getActiveConnections(): Thenable<sqlops.connection.Connection[]>` Ottiene un elenco delle connessioni dell'utente che sono attive. Restituisce un elenco vuoto se non sono presenti tali connessioni.

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` Ottiene un dizionario contenente le credenziali associate a una connessione. In caso contrario essere restituiti come parte del dizionario opzioni sotto un `sqlops.connection.Connection` oggetto ma ottenere rimossi da tale oggetto. 

### `Connection`
- `options: { [name: string]: string }` Il dizionario delle opzioni di connessione
- `providerName: string` Il nome del provider di connessione (ad esempio, "MSSQL")
- `connectionId: string` L'identificatore univoco per la connessione

### <a name="example-code"></a>Codice di esempio
```
> let connection = sqlops.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = sqlops.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>Esplora oggetti

`sqlops.objectexplorer`


### <a name="top-level-functions"></a>Funzioni di primo livello
- `getNode(connectionId: string, nodePath?: string): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Ottenere un nodo Esplora oggetti corrispondente alla connessione specificata e il percorso. Se non viene specificato alcun percorso, viene restituito il nodo di primo livello per la connessione specificata. Se non è presente alcun nodo nel percorso specificato, verrà restituito `undefined`. Nota: Il `nodePath` per un oggetto generato dal back-end di servizio di strumenti di SQL ed è difficile da costruire manualmente. Futuri miglioramenti dell'API consentirà di ottenere i nodi in base ai metadati forniti in merito al nodo, ad esempio nome, tipo e dello schema.

- `getActiveConnectionNodes(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Ottenere tutti i nodi di connessione di Esplora oggetti attivi.

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` Trovare tutti i nodi di Esplora oggetti che corrispondono ai metadati specificato. Il `schema`, `database`, e `parentObjectNames` gli argomenti devono essere `undefined` quando non sono applicabili. `parentObjectNames` è un elenco di oggetti padre non di database, dal prezzo massimo al livello più basso in Esplora oggetti, in cui l'oggetto desiderato. Ad esempio, durante la ricerca di una colonna "column1" che appartiene a una tabella "schema1.table1" e il database "database1" con ID di connessione `connectionId`, chiamare `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`. Vedere anche il [elenco di tipi che per impostazione predefinita Azure Data Studio supporta](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API) per questa chiamata API.

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` L'id della connessione che il nodo è presente in

- `nodePath: string` Il percorso del nodo, come nel caso una chiamata al `getNode` (funzione).

- `nodeType: string` Stringa che rappresenta il tipo del nodo

- `nodeSubType: string` Stringa che rappresenta il sottotipo del nodo

- `nodeStatus: string` Stringa che rappresenta lo stato del nodo

- `label: string` L'etichetta per il nodo che viene visualizzata in Esplora oggetti

- `isLeaf: boolean` Indica se il nodo è un nodo foglia e pertanto non ha elementi figlio

- `metadata: sqlops.ObjectMetadata` Metadati che descrivono l'oggetto rappresentato da questo nodo

- `errorMessage: string` Messaggio visualizzato se il nodo è in stato di errore

- `isExpanded(): Thenable<boolean>` Se il nodo è correntemente espanso in Esplora oggetti

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` Specificare se il nodo è espanso o compresso. Se lo stato viene impostato su None, il nodo non cambierà.

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` Specificare se si seleziona il nodo. Se `clearOtherSelections` è true, deselezionare tutte le altre selezioni quando si effettua la nuova selezione. Se è false, lasciare le selezioni esistenti. `clearOtherSelections` il valore predefinito è true quando `selected` è true e false se `selected` è false.

- `getChildren(): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` Ottenere tutti gli elementi figlio del nodo. Restituisce un elenco vuoto se non sono presenti elementi figlio.

- `getParent(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Ottenere il nodo padre di questo nodo. Restituisce non definito se non esiste alcun padre.

### <a name="example-code"></a>Codice di esempio

```cs
private async interactWithOENode(selectedNode: sqlops.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: sqlops.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await sqlops.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    sqlops.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>API proposte

Sono state aggiunte API proposte per consentire le estensioni visualizzare l'interfaccia utente personalizzata in schede dei documenti, tra le altre funzionalità, le procedure guidate e finestre di dialogo. Vedere le [proposto i file di tipi di API](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.proposed.d.ts) per altra documentazione, tuttavia tenere presente che queste API sono soggetti a modifiche in qualsiasi momento. Esempi di come utilizzare alcune di queste API sono reperibili nel [estensione di esempio "sqlservices"](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices).


