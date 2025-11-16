---
title: Permission Management
description: Control access to documentation spaces
order: 3
---

# Permission Management

Control who can view, edit, and manage documentation spaces with Docify's role-based access control.

## Role Types

### Viewer

**Can:**

- View all published documents
- Use search functionality
- Access public spaces

**Cannot:**

- Modify or create documents
- Access admin settings
- Manage permissions

### Editor

**Can:**

- View all documents
- Create new documents
- Edit existing documents
- Access document history

**Cannot:**

- Change space settings
- Manage user permissions
- Configure repository sync
- Delete documents (typically)

### Admin

**Can:**

- View, create, and edit documents
- Manage all space settings
- Configure repository sync
- Assign roles and manage permissions
- Delete spaces and documents
- View audit logs

## Managing Team Access

### Adding Members

1. Go to **Space Settings** → **Team**
2. Click **Add Member**
3. Enter GitHub username or email
4. Select role (Viewer, Editor, Admin)
5. Click **Invite**

### Changing Roles

1. Find member in team list
2. Click the role dropdown
3. Select new role
4. Confirm change

### Removing Members

1. Find member in team list
2. Click **Remove** (icon)
3. Confirm removal

## Permission Matrix

| Action          | Viewer | Editor | Admin |
| --------------- | ------ | ------ | ----- |
| View docs       | ✅     | ✅     | ✅    |
| Search          | ✅     | ✅     | ✅    |
| Create docs     | ❌     | ✅     | ✅    |
| Edit docs       | ❌     | ✅     | ✅    |
| Delete docs     | ❌     | ❌     | ✅    |
| Manage team     | ❌     | ❌     | ✅    |
| Configure sync  | ❌     | ❌     | ✅    |
| Change settings | ❌     | ❌     | ✅    |
| Delete space    | ❌     | ❌     | ✅    |

## Best Practices

### Principle of Least Privilege

Only grant the minimum permissions needed:

```
✅ Technical writer → Editor
✅ Project manager → Viewer
✅ Team lead → Admin
✅ CI/CD system → Viewer (if automated)
```

### Separate Admin Access

- Avoid giving everyone admin access
- Designate 2-3 team admins
- Rotate admin responsibilities periodically

### Documentation Leads

- Assign one "documentation lead" per space
- Give them admin access
- Responsible for quality and consistency

### Regular Audits

1. Monthly: Review team access levels
2. Quarterly: Audit who has admin access
3. When someone leaves: Revoke access immediately

## Default Roles

### New Space

When creating a space, set default viewer access:

```
Public: Disabled (only invited users)
Default role for new members: Viewer
```

### Organization-wide

Configure organization defaults in Admin Settings:

```
New members join as: Viewer
Auto-add to new spaces: Yes/No
```

## Sharing Documentation

### Public vs Private

**Private Space** (Default)

- Only invited members can access
- More secure for internal docs
- Full access control

**Public Space** (Optional)

- Anyone with the link can view
- No login required
- Good for external documentation

### Sharing Links

Generate read-only links for external stakeholders:

```
https://docify.company.com/spaces/api-docs?token=xxx
Expires: 30 days
```

## Audit & Logging

### Access Logs

View who accessed what and when:

1. Go to **Settings** → **Audit Log**
2. Filter by date, user, or action
3. Export for compliance

### Actions Logged

- Login/logout
- Document viewed
- Document edited
- Permissions changed
- Space configured

### Retention

- Standard: 90 days
- Enterprise: 1 year (configurable)

## Troubleshooting

### User Can't Access Space

1. Verify user role is not "Removed"
2. Check if space is public or requires invite
3. Verify user account is activated
4. Check audit log for errors

### Can't Change Someone's Role

1. Verify you have admin access
2. Verify the user account exists
3. Check if they're part of the team

---

**More Help?** Contact your workspace admin or check [Support](../troubleshooting/).
