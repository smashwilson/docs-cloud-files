
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

Create or update container metadata
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1/{account}/{container}

Creates or updates the container metadata by associating custom metadata headers with the container-level URI. These headers must have the format ``X-Container-Meta-name``.

To set or edit container metadata, perform a ``POST`` operation to the container. The operation must include ``X-Container-Meta-name``, where ``name`` is the name of your custom metadata. Subsequent ``POST`` operations to the header using the same metadata name overwrite the previous value. 

To view your metadata changes, perform a ``HEAD`` operation on the container. (For more information, see `Show container metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/HEAD_retrievecontainermeta_v1__account___container__containerServicesOperations_d1e000.html>`__.) Do not try to send the metadata in your ``HEAD`` request. 

Updating container metadataFor containers, the ``POST`` request to set metadata does not delete existing metadata that is not explicitly set in the request.

For example, you use a ``HEAD`` request to list container metadata and get the following results:

X-Container-Meta-Price: 50                    X-Container-Meta-Extra: DataThen you perform a ``POST`` request similar to the following example to set metadata on the same container that you listed above:

POST /v1/account/containName HTTP/1.1Host: storage.clouddrive.comX-Auth-Token: yourAuthTokenX-Container-Meta-Price: 45X-Container-Meta-Cost: 30Listing the container metadata again after the ``POST`` then shows the following results. The ``X-Container-Meta-Extra`` metadata still exists.

X-Container-Meta-Price: 45                    X-Container-Meta-Cost: 30X-Container-Meta-Extra: DataFor information about deleting container metadata, see `Create or update container metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/POST_updateacontainermeta_v1__account___container__containerServicesOperations_d1e000.html>`__.

Note that updating and deleting object metadata works differently. For an example, see `Chapter 7. Additional container services information <http://docs.rackspace.com/files/api/v1/cf-devguide/content/containerMetadataOptions_d1e001.html>`__.

A status code of 204 (No Content) indicates success. Status code 404 (Not Found) is returned when the requested container does not exist.

This operation does not require a request body and does not return a response body.

.. note::
   For information about adding metadata for the following purposes, see `Get object content and metadata <http://docs.rackspace.com/files/api/v1/cf-devguide/content/GET_getobjectdata_v1__account___container___object__objectServicesOperations_d1e000.html>`__ : 
   
    
   
   *  Container quotas
   *  Access log delivery
   
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|204                       |No Content               |The request succeeded.   |
|                          |                         |The server fulfilled the |
|                          |                         |request but does not     |
|                          |                         |need to return a         |
|                          |                         |body.The length of the   |
|                          |                         |response body that       |
|                          |                         |contains the list of     |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |length of the error text |
|                          |                         |in the response body.The |
|                          |                         |MIME type of the list of |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |MIME type of the error   |
|                          |                         |text in the response     |
|                          |                         |body.A unique            |
|                          |                         |transaction identifier   |
|                          |                         |for this request.The     |
|                          |                         |transaction date and     |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested resource   |
|                          |                         |was not found.           |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""


This table shows the header parameters for the request:

+------------+-------------+---------------------------------------------------+
|Name        |Type         |Description                                        |
+============+=============+===================================================+
|X-Auth-Token|String       |Authentication token.                              |
|            |*(Required)* |                                                   |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |The container metadata. Replace ``name`` at the    |
|Meta-name   |*(Required)* |end of the header with the name of your metadata.  |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Sets an access control list (ACL) that grants read |
|Read        |*(Optional)* |access. This header can contain a comma-delimited  |
|            |             |list of users that can read the container (allows  |
|            |             |the GET method for all objects in the container).  |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Sets an ACL that grants write access. This header  |
|Write       |*(Optional)* |can contain a comma-delimited list of users that   |
|            |             |can write to the container (allows PUT, POST,      |
|            |             |COPY, and DELETE methods for all objects in the    |
|            |             |container).                                        |
+------------+-------------+---------------------------------------------------+
|X-Remove-   |String       |Removes the metadata item named metadata. For      |
|Container-  |*(Optional)* |example, X-Remove-Container-Read removes the X-    |
|name        |             |Container-Read metadata item.                      |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Sets the destination for container                 |
|Sync-To     |*(Optional)* |synchronization. For container synchronization,    |
|            |             |the ``X-Container-Sync-To`` value must follow the  |
|            |             |form                                               |
|            |             |//realmName/clusterName/accountName/containerName. |
+------------+-------------+---------------------------------------------------+
|X-Container-|String       |Sets the secret key for container synchronization. |
|Sync-Key    |*(Optional)* |For container synchronization, you must set ``X-   |
|            |             |Container-Sync-Key`` on the source container and   |
|            |             |the destination container.                         |
+------------+-------------+---------------------------------------------------+
|X-Versions- |String       |Enables versioning on this container. The value is |
|Location    |*(Optional)* |the name of another container. You must UTF-8-     |
|            |             |encode and then URL-encode the name before you     |
|            |             |include it in the header. To disable versioning,   |
|            |             |set the header to an empty string.                 |
+------------+-------------+---------------------------------------------------+
|X-Remove-   |String       |Set to any value to disable versioning.            |
|Versions-   |*(Optional)* |                                                   |
|Location    |             |                                                   |
+------------+-------------+---------------------------------------------------+
|Content-Type|String       |Changes the MIME type for the object.              |
|            |*(Optional)* |                                                   |
+------------+-------------+---------------------------------------------------+
|X-Detect-   |Boolean      |If set to ``True``, Cloud Files guesses the        |
|Content-Type|*(Optional)* |content type based on the file extension and       |
|            |             |ignores the value sent in the ``Content-Type``     |
|            |             |header, if present.                                |
+------------+-------------+---------------------------------------------------+




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |Your unique account      |
|                          |                         |identifier.              |
+--------------------------+-------------------------+-------------------------+
|{container}               |String                   |The unique identifier of |
|                          |                         |the container.           |
+--------------------------+-------------------------+-------------------------+





This operation does not accept a request body.




**Example Create or update container metadata: HTTP request**


.. code::

    POST /v1/MossoCloudFS_0672d7fa-9f85-4a81-a3ab-adb66a880123/MyContainer HTTP/
    1.1
    Host: storage.clouddrive.com
    X-Auth-Token: f064c46a782c444cb4ba4b6434288f7c
    X-Container-Meta-Book: MobyDick
    X-Container-Meta-Subject: Whaling


Response
""""""""""""""""


This table shows the header parameters for the response:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|Content-Length            |String *(Required)*      |The length of the        |
|                          |                         |response body that       |
|                          |                         |contains the list of     |
|                          |                         |names. If the operation  |
|                          |                         |fails, this value is the |
|                          |                         |length of the error text |
|                          |                         |in the response body.    |
+--------------------------+-------------------------+-------------------------+
|Content-Type              |String *(Required)*      |The MIME type of the     |
|                          |                         |list of names. If the    |
|                          |                         |operation fails, this    |
|                          |                         |value is the MIME type   |
|                          |                         |of the error text in the |
|                          |                         |response body.           |
+--------------------------+-------------------------+-------------------------+
|X-Trans-Id                |Uuid *(Required)*        |A unique transaction     |
|                          |                         |identifier for this      |
|                          |                         |request.                 |
+--------------------------+-------------------------+-------------------------+
|Date                      |Datetime *(Required)*    |The transaction date and |
|                          |                         |time.                    |
+--------------------------+-------------------------+-------------------------+







**Example Create or update container metadata: HTTP response**


.. code::

    HTTP/1.1 204 No Content
    Content-Length: 0
    Content-Type: text/html; charset=UTF-8
    X-Trans-Id: tx05dbd434c651429193139-0052d82635
    Date: Thu, 16 Jan 2014 18:34:29 GMT


