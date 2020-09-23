# GPG

## Show existing key

    gpg --list-key [key-id]

## Edit existing key

    gpg --edit-key [key-id]

### Edit options on gpg command line

    trust  // Change owner trust
    expire // Change expiration time
    save   // Save all changes
    quit   // Quit without saving

## Export public key

    gpg --export -a [key-id] > public.asc

## Export private key

    gpg --export-secret-keys -a [key-id] > private.asc

## Import public key

    gpg --import public.asc

## Import private key

    gpg --import private.key
