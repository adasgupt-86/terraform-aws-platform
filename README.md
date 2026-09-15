# Terraform AWS Platform

Terraform infrastructure managed through GitHub and Jenkins.

## Structure

- environments/dev - Development environment
- modules - Reusable Terraform modules
- tests - Terraform tests

## Workflow

GitHub -> Jenkins -> Terraform Plan -> Approval -> Terraform Apply

## AWS Region

ap-south-1

## Terraform

Terraform configuration is validated and deployed through CI/CD.
