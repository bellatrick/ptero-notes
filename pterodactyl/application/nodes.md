### Example Model

```json
{
  "allocated_resources": {
    "disk": 26512,
    "memory": 12368
  },
  "behind_proxy": false,
  "created_at": "2022-01-03T09:25:00+00:00",
  "daemon_base": "/var/lib/pterodactyl/volumes",
  "daemon_listen": 7373,
  "daemon_sftp": 3033,
  "description": "ptero test node",
  "disk": 72000,
  "disk_overallocate": -1,
  "fqdn": "nodes.pterodactyl.test",
  "id": 1,
  "location_id": 1,
  "maintenance_mode": false,
  "memory": 16000,
  "memory_overallocate": -1,
  "name": "ID1",
  "public": true,
  "scheme": "https",
  "updated_at": "2022-08-25T10:49:25+00:00",
  "upload_size": 100,
  "uuid": "21412d5d-4f65-4ba8-8803-6e1754b9b4e6"
}
```

### `GET /nodes`

Returns a list of node objects.

### Parameters

| Name     | Supported | Allowed Values                    |
| -------- | --------- | --------------------------------- |
| filter   | ✅        | daemon_token_id, fqdn, name, uuid |
| include  | ✅        | allocations, locations, servers   |
| sort     | ✅        | disk, id, memory, uuid            |
| page     | ✅        | Any number                        |
| per_page | ✅        | Any number                        |

### `GET /nodes/deployable`

Returns a list of deployable nodes.

### Parameters

| Name     | Supported | Allowed Values |
| -------- | --------- | -------------- |
| filter   | ❌        |
| include  | ❌        |
| sort     | ❌        |
| page     | ✅        | Any number     |
| per_page | ✅        | Any number     |

### Body

| Key          | Required | Type       | Description                              |
| ------------ | -------- | ---------- | ---------------------------------------- |
| disk         | ✅       | `number`   | The disk limit to query nodes by         |
| memory       | ✅       | `number`   | The memory limit to query nodes by       |
| location_ids | ❌       | `number[]` | A list of location IDs to query nodes by |
| page         | ❌       | `number`   | N/A                                      |

### `GET /nodes/:id`

Returns a node by its `id` (number). Supports the above "include" parameter.

### `GET /nodes/:id/allocations`

Returns a list of allocations on the node.

### Parameters

| Name     | Supported | Allowed Values                |
| -------- | --------- | ----------------------------- |
| filter   | ✅        | ip, ip_alias, port, server_id |
| include  | ✅        | node, server                  |
| sort     | ❌        |
| page     | ✅        | Any number                    |
| per_page | ✅        | Any number                    |

### `POST /nodes/:id/allocations`

Creates an allocation on the node.

### Body

| Key   | Required | Type       | Description                                        |
| ----- | -------- | ---------- | -------------------------------------------------- |
| ip    | ✅       | `string`   | The IP to bind the allocation to                   |
| alias | ❌       | `string`   | The IP alias for the allocation                    |
| ports | ✅       | `string[]` | A list of ports or port-ranges for the allocation. |

### `DELETE /nodes/:id/allocations/:id`

Deletes an allocation from the node by its `id` (number).

### `GET /nodes/:id/configuration`

Returns the configuration data of a specified node.

### `POST /nodes`

Creates a node.

### Body

| Key                 | Required | Type      | Description                                                    |
| ------------------- | -------- | --------- | -------------------------------------------------------------- |
| behind_proxy        | ✅       | `boolean` | Whether the node is behind a proxy                             |
| daemon_base         | ✅       | `string`  | The daemon base for the node                                   |
| daemon_listen       | ✅       | `number`  | The port for the daemon to listen on                           |
| daemon_sftp         | ✅       | `number`  | The SFTP port for the node                                     |
| description         | ❌       | `string`  | A description of the node                                      |
| disk                | ✅       | `string`  | The disk space limit                                           |
| disk_overallocate   | ✅       | `string`  | The overallocated disk space limit                             |
| fqdn                | ✅       | `string`  | The FQDN of the node                                           |
| location_id         | ✅       | `number`  | The location to create the node on                             |
| maintenance_mode    | ❌       | `boolean` | Whether the node should be under maintenance mode when created |
| memory              | ✅       | `number`  | The memory usage limit                                         |
| memory_overallocate | ✅       | `string`  | The overallocated memory limit                                 |
| name                | ✅       | `string`  | The name of the node                                           |
| public              | ❌       | `boolean` | Whether the node is publicly accessible                        |
| scheme              | ✅       | `string`  | The HTTP scheme for the node                                   |
| upload_size         | ❌       | `number`  | The upload size for the node                                   |

### `PATCH /nodes/:id`

Updates a node by its `id` (number).

### Body

| Key                 | Required | Type      | Description                                                    |
| ------------------- | -------- | --------- | -------------------------------------------------------------- |
| behind_proxy        | ❌       | `boolean` | Whether the node is behind a proxy                             |
| daemon_base         | ❌       | `string`  | The daemon base for the node                                   |
| daemon_listen       | ❌       | `number`  | The port for the daemon to listen on                           |
| daemon_sftp         | ❌       | `number`  | The SFTP port for the node                                     |
| description         | ❌       | `string`  | A description of the node                                      |
| disk                | ❌       | `string`  | The disk space limit                                           |
| disk_overallocate   | ❌       | `string`  | The overallocated disk space limit                             |
| fqdn                | ❌       | `string`  | The FQDN of the node                                           |
| location_id         | ❌       | `number`  | The location to create the node on                             |
| maintenance_mode    | ❌       | `boolean` | Whether the node should be under maintenance mode when created |
| memory              | ❌       | `number`  | The memory usage limit                                         |
| memory_overallocate | ❌       | `string`  | The overallocated memory limit                                 |
| name                | ❌       | `string`  | The name of the node                                           |
| public              | ❌       | `boolean` | Whether the node is publicly accessible                        |
| scheme              | ❌       | `string`  | The HTTP scheme for the node                                   |
| upload_size         | ❌       | `number`  | The upload size for the node                                   |

### `DELETE /nodes/:id`

Deletes a node by its `id` (number).
