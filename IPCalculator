''' Trabalho realizado como avaliação do segundo NAP da disciplina Rede de Computadores I em conjunto com as disciplina Estrutura de dados I
Aluna: Bruna Costa de Souza
'''
import re

class Ipv4Calculator:
    """Obtém todos os dados de uma rede IPv4"""

    __slots__ = ('_ip', '_mascara', '_prefixo', '_broadcast',
                 '_numero_ips', '_rede', '_ip_bin', '_mascara_bin',
                 '_rede_bin', '_broadcast_bin',)

    def __init__(self, ip: str = '', prefixo: int = 0, mascara: str = ''):
        """Configura os parâmetros e executa """
        if ip:
            self._reset()
            self.ip: str = ip
        else:
            self.ip: str = ''

        if prefixo:
            self.prefixo: int = prefixo
        else:
            self.prefixo: int = 0

        if mascara:
            self.mascara: str = mascara
        else:
            self.mascara: str = ''

        self._rede: str = ''
        self._broadcast: str = ''
        self._numero_ips: int = 0
			

        # Executa tudo caso o IP tenha sido enviado
        self.run()

    def _reset(self):
        """Nos casos de reutilização, zera os valores dos
        atributos e propriedades"""
        self._ip: str = ''
        self._mascara: str = ''
        self._prefixo: int = 0
        self._broadcast: str = ''
        self._rede: str = ''
        self._numero_ips: int = 0
				

    def run(self):
        """Realiza os cálculos
        """



        # Extrai o prefixo do IP caso IP tenha o formato IP/CIDR
        self._set_numero_ips()
        self._set_rede_broadcast()
        self._set_mascara_do_prefixo()

    def _set_mascara_do_prefixo(self):
        """Configura O IP da máscara usando o prefixo."""
        mascara_bits = self.prefixo * str('1')
        host_bits = (32 - self.prefixo) * str('0')

        self._mascara_bin = self._binario_adiciona_pontos(
            mascara_bits + host_bits)

        # Converte a máscara para decimal
        mascara_dec: str = self._ip_binario_para_decimal(self._mascara_bin)
        self._mascara: str = mascara_dec

    def _set_rede_broadcast(self):
        """Configura rede e broadcast"""
        ip_bin: str = self._ip_decimal_para_binario(self.ip)
        ip_bin: str = ip_bin.replace('.', '')

        ip_bits = ip_bin[:self._prefixo]
        host_bits = 32 - self.prefixo
        rede = ip_bits + (str('0') * host_bits)
        broadcast = ip_bits + (str('1') * host_bits)

        self._ip_bin = self._binario_adiciona_pontos(ip_bin)
        self._rede_bin = self._binario_adiciona_pontos(rede)
        self._broadcast_bin = self._binario_adiciona_pontos(broadcast)

        self._rede: str = self._ip_binario_para_decimal(rede)
        self._broadcast: str = self._ip_binario_para_decimal(broadcast)

    def _binario_adiciona_pontos(self, b: str) -> str:
        """Adiciona pontos aos octetos"""
        b: str = re.sub('[^0-1]', '', b)
        return f'{b[0:8]}.{b[8:16]}.{b[16:24]}.{b[24:32]}'

    def _set_numero_ips(self):
        """Configura o número de hosts para a rede"""
        host_bits: int = 32 - int(self._prefixo)
        self._numero_ips: int = pow(2, host_bits)
			
    def _ip_binario_para_decimal(self, ip: str = '') -> str:
        """Converte um IP binário para decimal """
        ip: str = re.sub('[^0-9]', '', ip)

        novo_ip: str = str(int(ip[0:8], 2)) + '.'
        novo_ip += str(int(ip[8:16], 2)) + '.'
        novo_ip += str(int(ip[16:24], 2)) + '.'
        novo_ip += str(int(ip[24:32], 2))

        return novo_ip

    def _ip_decimal_para_binario(self, ip: str = '') -> str:
        """Converte um IP decimal para binário"""
        if not ip:
            ip: str = self.ip

        # Divide o IP em 4 blocos
        bloco_ip: list = ip.split('.')
        ip_bin: list = []

        for bloco in bloco_ip:
            # Converte o bloco para binário
            binario: bin = bin(int(bloco))
            # Forma o octeto
            binario: bin = binario[2:].zfill(8)
            ip_bin.append(binario)

        ip_bin: str = '.'.join(ip_bin)
        return ip_bin


    # GETTERS
    @property
    def ip(self) -> str:
        return str(self._ip)

    @property
    def prefixo(self) -> int:
        return int(self._prefixo)

    @property
    def mascara(self) -> str:
        return str(self._mascara)

    # Read only
    @property
    def rede(self) -> str:
        self._check_property(self._rede)
        return str(self._rede)

    @property
    def broadcast(self) -> str:
        self._check_property(self._broadcast)
        return str(self._broadcast)

    @property
    def numero_ips(self) -> str:
        self._check_property(self._numero_ips)
        return str(self._numero_ips)
		
    @property
    def ip_bin(self) -> str:
        self._check_property(self._ip_bin)
        return str(self._ip_bin)

    @property
    def mascara_bin(self) -> str:
        self._check_property(self._mascara_bin)
        return str(self._mascara_bin)

    @property
    def rede_bin(self) -> str:
        self._check_property(self._rede_bin)
        return str(self._rede_bin)

    @property
    def broadcast_bin(self) -> str:
        self._check_property(self._broadcast_bin)
        return str(self._broadcast)

    def get_all(self):
        """ Retorna tudo que foi configurado, caso necessário"""
        all: dict = {
            'ip': self.ip,
            'prefixo': self._prefixo,
            'mascara': self._mascara,
            'rede': self._rede,
            'broadcast': self._broadcast,
            'numero_ips': self._numero_ips,
						
        }

        return all

    def get_all_bin(self):
        """ Retorna tudo que foi configurado em binário"""
        all: dict = {
            'ip': self._ip_bin,
            'mascara': self._mascara_bin,
            'rede': self._rede_bin,
            'broadcast': self._broadcast_bin,
        }

        return all

    # SETTERS
    @ip.setter
    def ip(self, ip: str = ''):
        if ip:
            self._reset()
            self._ip: str = str(ip)
        else:
            self._ip = ''

    @prefixo.setter
    def prefixo(self, prefixo: int = 0):
        if prefixo:
            self._prefixo: int = int(prefixo)
        else:
            self._prefixo = 0

    @mascara.setter
    def mascara(self, mascara: str = ''):
        if mascara:
            self._mascara: str = str(mascara)
        else:
            self._mascara = ''


# Dados da rede
if __name__ == '__main__':
	#dados em binário
    dados = Ipv4Calculator(ip='192.168.10.200', prefixo=26)
    dados_bin: dict = dados.get_all_bin()
    dados_dec: dict = dados.get_all()
    print("Exibindo dados em binário ")
    print(dados_bin)
    print(dados_dec)
  
		#coding: utf-8
class HashLinearColisao:

     def __init__(self,tam):
          self.tab = {}
          self.tam_max = tam

     def funcaohash(self, chave):
          v = int(chave)
          return (v%int(self.tam_max))

     def cheia(self):
          return len(self.tab) == self.tam_max

     def imprime(self):
          for i in self.tab:
               print("Hash[%d] = 192.168.10." %i, end="")
							
               print (self.tab[i])
     
     def busca(self, chave):
          pos = self.funcaohash(chave)
          if self.tab.get(pos) == None: # se esta posição não existe
               return -1 #saida imediata
          if self.tab[pos] == chave: # se o item esta na posição indicada pela função hash
               return pos
          else:
               for i in self.tab: # busca do item em toda hash (pois ele pode ter sido inserido apos colisão)
                    if self.tab[i]==chave:
                         return i
          return -1

     def insere(self, item):
          if self.cheia():
               print("-> ATENÇÃO Tabela Hash CHEIA")
               return
          pos = self.funcaohash(item)
          if self.tab.get(pos) == None: # se posicao vazia
               self.tab[pos] = item
               print("-> Inserido HASH[%d]" %pos)
          else: # se posicao ocupada
               print("-> Ocorreu uma colisao na posicao %d" %pos)
               while True:
                    if self.tab[pos] == item: # se o item ja foi cadastrado
                         print("-> ATENCAO Esse item ja foi cadastrado")
                         return
                    if pos == (self.tam_max - 1):
                         pos = -1
                    pos = pos + 1 # incrementa mais uma posição
                    if self.tab.get(pos) == None:
                         self.tab[pos] = item
                         print("-> Inserido apos colisao HASH[%d]" %pos)
                         break              
# fim Classe HashLinearColisao
item = 0
tamanhoHash = 62
tab = HashLinearColisao(tamanhoHash)
print("\n****************************************************")
print("      Tabela HASH Colisoes Linear (%d itens) " %tamanhoHash)
print("****************************************************")
for i in range (192,254):
		item= i + 1
		item = tab.insere(item)
		

    
print("\nImprimindo conteudo")
tab.imprime()
print("\n")
