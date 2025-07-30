# CustomerApi

A .NET 8 Web API for managing customer data with Entity Framework Core and SQL Server.

## Features

- RESTful API endpoints for CRUD operations on customers
- Entity Framework Core with SQL Server
- Swagger/OpenAPI documentation
- Azure deployment ready

## API Endpoints

- `GET /customers` - Get all customers
- `GET /customers/{id}` - Get customer by ID
- `POST /customers` - Create new customer
- `PUT /customers/{id}` - Update customer
- `DELETE /customers/{id}` - Delete customer

## Local Development

1. Clone the repository
2. Update connection string in `appsettings.json`
3. Run migrations: `dotnet ef database update`
4. Start the application: `dotnet run`
5. Access Swagger UI at: `http://localhost:5000`

## CI/CD Pipeline Setup

This project includes GitHub Actions workflows for automated build, test, and deployment to Azure.

### Workflows

1. **Build and Test** (`build-test.yml`)
   - Triggers on push to main/master branch
   - Restores dependencies
   - Builds the application
   - Runs tests

2. **Deploy to Azure** (`deploy-azure.yml`)
   - Triggers after successful build/test
   - Can also be triggered manually
   - Deploys to Azure Web App

### Setup Instructions

1. **Get Azure Publish Profile**:
   ```bash
   az webapp deployment list-publishing-profiles --name customer-api-app-nazar123 --resource-group myResourceGroup --xml
   ```

2. **Add GitHub Secret**:
   - Go to your GitHub repository
   - Navigate to Settings > Secrets and variables > Actions
   - Add new repository secret:
     - Name: `AZURE_WEBAPP_PUBLISH_PROFILE`
     - Value: Copy the entire XML content from the publish profile

3. **Enable GitHub Actions**:
   - Push these workflow files to your repository
   - GitHub Actions will automatically start working

### Manual Deployment

To deploy manually:
1. Go to Actions tab in GitHub
2. Select "Deploy to Azure" workflow
3. Click "Run workflow"
4. Select branch and click "Run workflow"

## Azure Resources

- **Web App**: customer-api-app-nazar123
- **Resource Group**: myResourceGroup
- **App Service Plan**: myLinuxPlan
- **Runtime**: .NET Core 8.0 (Linux)

## Database

The application uses Entity Framework Core with SQL Server. Make sure to:
1. Update the connection string in Azure App Settings
2. Run migrations on the Azure database

## Contributing

1. Create a feature branch
2. Make your changes
3. Push to your branch
4. Create a pull request
5. CI/CD pipeline will automatically build and test 