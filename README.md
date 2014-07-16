StaleMate: A Web API for Messages That Expire
==========================================

Roles
=====

Application: APPID
   an authenticated application can utilize the api to create & spread 
   StaleMate messages

   An application is authenticated with its private (PRI) / 
   public key pair (PUB)

   An application saves its private key; the servers use the public
key to verify the application. We may need some sort of session-key
mechanism.

   The application encrypts a message before pushing it to the server;
   the encrypt private key is abandoned after use; (no forge)

   The application broadcasts (through a user chosen method, e.g. email or
WeiBo/ WeChat / Twitter / Facebook) the access URL of the message.

Publisher: (https)
   The servers that accept application requests; 
   messages are pushed to publishers; 
   publisher and application negotiate a key pair, and message is
encrypted by the application before entering the publisher;
   The publisher then push the messages to the Data Server; 

Message Board: (https)
   The servers that provide access to StaleMate messages.
   Translate the URL of a message to the public key to decrypt the
message;
   Translate the URL of a message to the data server entry.
   Fetch the entry, decrypt and return the message context
   If a message is expired, report 404; queue it for purge.
   Caching: Maintain a list of recently accessed expired message;
      never cache the content.

Data Server: (internal cloud network)
   Accounting information: how many times a message is accessed.
   Where messages are saved; can be a cloud file storage service.
   Periodically purge the expired messages.

