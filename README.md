# Scripts
#CÁLCULO DO HASH RATE DA REDE BITCOIN
#import requests
==================================================
CÁLCULO DO HASH RATE DA REDE BITCOIN
==================================================
Dificuldade Atual: 83,126,984,677,668
Tempo Médio do Bloco: 600.50 segundos
Hash Rate Estimado: 594.25 EH/s
Hash Rate Bruto: 5.94e+20 H/s
==================================================

#Instale a biblioteca requests (se ainda não tiver):
#pip install requests
#Execute o script
#python hashrate_calculator.py
python
def calcular_hash_rate():
    """
   # Calcula o hash rate estimado da rede Bitcoin (em EH/s) com base na dificuldade atual e no tempo médio de bloco.
    #Fonte dos dados: Blockchain.com API
    """
    # Constante: número médio de hashes para encontrar um nonce válido
    CONSTANTE_2_32 = 2**32  # 4.294.967.296

    try:
        # Fetch dados atuais da rede Bitcoin
        url = 'https://blockchain.info/q'
        dificuldade = float(requests.get(url + '/getdifficulty').text)
        tempo_medio_bloco = float(requests.get(url + '/interval').text)  # em segundos

        # Fórmula: Hash Rate = (Dificuldade * 2^32) / Tempo Médio do Bloco
        hash_rate_hs = (dificuldade * CONSTANTE_2_32) / tempo_medio_bloco

        # Convertendo para Exahashes por segundo (EH/s)
        hash_rate_ehs = hash_rate_hs / 1e18

        # Exibindo resultados
        print("\n" + "="*50)
        print("CÁLCULO DO HASH RATE DA REDE BITCOIN")
        print("="*50)
        print(f"Dificuldade Atual: {dificuldade:,.0f}")
        print(f"Tempo Médio do Bloco: {tempo_medio_bloco:.2f} segundos")
        print(f"Hash Rate Estimado: {hash_rate_ehs:.2f} EH/s")
        print(f"Hash Rate Bruto: {hash_rate_hs:.2e} H/s")
        print("="*50)

    except Exception as e:
        print(f"Erro ao acessar API: {e}")

# Executar o script
if __name__ == "__main__":
    calcular_hash_rate()
    
