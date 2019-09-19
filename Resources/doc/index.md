Documentation
==============

Simple Example

        $config = ['type' => 'public_key',
                'host' => 'hostname,
                'username' => 'username',
                'public_key_file' => __DIR__ . '/../Files/'.$serverName.'/id_rsa.pub',
                'private_key_file' => __DIR__ . '/../Files/'.$serverName.'/id_rsa'];

        $factory = new SessionFactory();
        $session = $factory->getSession($config);

        $sftp = $session->getSftp();
        
        $destinationDir = "/tmp/test";
        if(!$sftp->exists($destinationDir)) { $sftp->mkdir($destinationDir, 0755); }
        
        $destinationFile = $destinationDir."/testfile";
        if($sftp->exists($destinationFile)) { $sftp->unlink($destinationFile); }
        $sftp->send($sourceFile, $destinationFile);
        
        $sftp->receive($destinationFile, $sourceFile.".val");
        
        $exec = $session->getExec();
        $exec->run('sudo rsync -raz --progress /tmp/test/ /tmp/test2/');
        