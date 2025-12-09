# USTHB Hub API Documentation

Welcome to the USTHB Hub API documentation. This API allows users to create, manage, and share educational resources for the university community.

## Features

- 📚 **Contribution Management**: Create and manage educational contributions
- 📄 **Resource Upload**: Upload PDFs and images with metadata
- ✅ **Admin Moderation**: Approve or reject submitted resources
- 👤 **User Authentication**: JWT-based authentication system
- 🔒 **Authorization**: Role-based access control (User/Admin)

## Base URL

```
https://your-api-domain.com
```

## Authentication

Most endpoints require authentication using JWT tokens. Include your token in the Authorization header:

```
Authorization: Bearer <your-token>
```

## Getting Started

1. [Register an account](api-reference/contributions.md#authentication)
2. [Login to get your token](api-reference/contributions.md#authentication)
3. [Create your first contribution](api-reference/contributions.md#create-contribution)

## API Reference

Browse the complete API documentation:

- [Contributions API](api-reference/contributions.md) - Complete reference for managing contributions and resources

## Support

For issues or questions, please contact the development team or create an issue on GitHub.
