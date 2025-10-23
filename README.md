# FGT
FGT - Fortigate

````js
cy.get('body').then(($body) => {
  if ($body.find('#option1').length > 0) {
    // option1 est présent
    cy.get('#option1').should('be.visible').click();
  } else {
    // sinon, option2
    cy.get('#option2').should('be.visible').click();
  }
});
````

<img src="https://i.imgur.com/zQcO3df.png">
<img src="https://i.imgur.com/tADTe2b.png">
<img src="https://i.imgur.com/QbXBgaI.png">
<img src="https://i.imgur.com/I8C0Z8e.png">
