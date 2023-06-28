name: apiTest
on:
  push:
    branches:
      - main
  workflow_dispatch:   
  
jobs:
  test-api:
    runs-on: ubuntu-latest
    steps:
      # INstall Node on the runner
      - name: Install Node
        uses: actions/checkout@v3
        with:
          node-version: "16.x"


      # Install the newman command line utility and also install the html extra reporter
      - name: Install newman
        run: |
          npm install -g newman
          npm install -g newman-reporter-htmlextra

      # Run the POSTMAN collection
      - name: Run POSTMAN collection
        run: |
          newman run demo.json --reporters cli,htmlextra --reporter-htmlextra-export index.html --reporter-htmlextra-darkTheme  
      # Upload the contents of Test Results directory to workspace
      - name: Output the run Details
        uses: actions/upload-artifact@v3
        if: always()
        continue-on-error: true
        with:
          name: RunReports
          path: index.html
