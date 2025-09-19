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
````yaml
jobs:
  ip-check:
    runs-on: self-hosted
    steps:
      - name: Generate unique marker
        id: marker
        run: |
          UUID=$(uuidgen)
          echo "uuid=$UUID" >> $GITHUB_OUTPUT

      - name: Send marker to GitHub (repository_dispatch)
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          uuid="${{ steps.marker.outputs.uuid }}"
          gh api repos/${{ github.repository }}/dispatches \
            -f event_type=ip-check \
            -f client_payload:="{\"uuid\":\"$uuid\"}"

  read-audit:
    needs: ip-check
    runs-on: ubuntu-latest   # ou un autre runner avec accès audit log
    steps:
      - name: Get marker
        run: echo "UUID=${{ needs.ip-check.outputs.uuid }}"

      - name: Query audit log
        env:
          GH_TOKEN: ${{ secrets.ORG_ADMIN_TOKEN }} # doit avoir accès audit log
        run: |
          uuid="${{ needs.ip-check.outputs.uuid }}"
          # récupérer les events de l’org et chercher ton UUID
          gh api /orgs/${{ github.repository_owner }}/audit-log \
            --paginate > audit.json
          jq -r --arg uuid "$uuid" '.[] | select(.action_message|contains($uuid)) | {actor_ip}' audit.json

````
