Zf2BcryptAuthAdapter
====================

Bcrypt auth adapter for ZF2


How to use:

1. Copy and add file BcryptDbAdapter.php to your project

2. Define you namespace for BcryptDbAdapter class instead of:
<pre>namespace Admin\Service\Auth\Adapter;</pre>

3. Example usage in controller:

<pre>
	
$data = $request->getPost();

$dbAdapter = $this->getServiceLocator()->get('Zend\Db\Adapter\Adapter');

$authAdapter = new AuthAdapter($dbAdapter);

$authAdapter
    ->setTableName('users')
    ->setIdentityColumn('email')
    ->setCredentialColumn('password');

$authAdapter
    ->setIdentity(addslashes($data['email']))
    ->setCredential($data['password']);

// attempt authentication
$result = $authAdapter->authenticate();

if (!$result->isValid()) {
    // Authentication failed
} else {
    $auth = new AuthenticationService();
    $storage = $auth->getStorage();

    $storage->write($authAdapter->getResultRowObject(
        null,
        'password'
    ));
}
</pre> 
