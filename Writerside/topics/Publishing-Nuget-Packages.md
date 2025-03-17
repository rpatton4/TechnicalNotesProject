# Publishing Nuget Packages

dotnet nuget add source --username rpatton@getfasolutions.com --password $GH_API_KEY --store-password-in-clear-text --name github "https://nuget.pkg.github.com/MySolfia/index.json"

dotnet nuget push CommonOriginationAndDisbursement.0.7.8.nupkg --api-key $GH_API_KEY --source "github"

