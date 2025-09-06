# FGT
FGT - Fortigate
````js
cy.document().then((doc) => {
        doc.body.innerHTML = `
          <h2>Résultat JSON</h2>
          <pre>${JSON.stringify(response.body, null, 2)}</pre>
        `;
      });
````
