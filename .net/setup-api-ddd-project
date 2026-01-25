#!/bin/bash

# Script para gerar estrutura de projeto C# API com DDD
# Recebe o nome do projeto como parâmetro

if [ -z "$1" ]; then
  echo "Uso: ./setup-api-ddd-project.sh NomeDoProjeto"
  exit 1
fi

projectName=$1

# Criar pastas raiz
mkdir -p src
mkdir -p tests

# Criar projetos dentro de src
dotnet new webapi -n "$projectName.API" -o "src/$projectName.API"
dotnet new classlib -n "$projectName.Application" -o "src/$projectName.Application"
dotnet new classlib -n "$projectName.Domain" -o "src/$projectName.Domain"
dotnet new classlib -n "$projectName.Infrastructure" -o "src/$projectName.Infrastructure"

# Criar projeto de testes
dotnet new xunit -n "$projectName.Tests" -o "tests/$projectName.Tests"

# Adicionar referências entre projetos
dotnet add "src/$projectName.API" reference "src/$projectName.Application"
dotnet add "src/$projectName.Application" reference "src/$projectName.Domain"
dotnet add "src/$projectName.Infrastructure" reference "src/$projectName.Domain"
dotnet add "src/$projectName.Application" reference "src/$projectName.Infrastructure"

# Referenciar Application e API nos testes
dotnet add "tests/$projectName.Tests" reference "src/$projectName.Application"
dotnet add "tests/$projectName.Tests" reference "src/$projectName.API"

# Criar solução
dotnet new sln -n "$projectName"

# Adicionar projetos à solução
dotnet sln "$projectName.sln" add "src/$projectName.API"
dotnet sln "$projectName.sln" add "src/$projectName.Application"
dotnet sln "$projectName.sln" add "src/$projectName.Domain"
dotnet sln "$projectName.sln" add "src/$projectName.Infrastructure"
dotnet sln "$projectName.sln" add "tests/$projectName.Tests"

echo "Estrutura DDD criada com sucesso para $projectName!"
