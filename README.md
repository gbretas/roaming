# roaming

Faz o hotspot do celular funcionar no Mac quando você está em roaming: a internet funciona no celular, mas não no computador conectado a ele.

## Instalar

```sh
sudo curl -fsSL https://raw.githubusercontent.com/gbretas/roaming/main/roaming -o /usr/local/bin/roaming
sudo chmod +x /usr/local/bin/roaming
```

## Usar

Conecte o Mac ao hotspot e rode:

```sh
roaming on      # liga a correção
roaming off     # volta ao padrão
roaming status  # mostra o TTL e o MTU atuais
```

Reiniciar o Mac também desfaz tudo.

## O que ele faz

- **TTL e hop limit 65:** os pacotes que passam pelo celular perdem 1 de TTL (64 vira 63), e a operadora usa isso para bloquear o compartilhamento. Com 65, eles chegam com 64 e parecem ter saído do próprio celular. Vale para IPv4 e IPv6.
- **MTU 1400:** em roaming, o tráfego volta ao país de origem por um túnel, e pacotes de 1500 bytes não passam. O sintoma é o ping funcionar e os sites ficarem carregando para sempre.

A mudança é aplicada na interface que está saindo para a internet no momento: Wi-Fi, USB ou Bluetooth.

## Ainda não funciona?

- **APN do hotspot vazio**
  - iPhone: Ajustes > Celular > Rede de Dados Celulares. Copie o APN de "Dados Celulares" para "Acesso Pessoal".
  - Android: no APN atual, acrescente `,dun` ao campo "Tipo de APN".
- **A operadora identifica o computador pelo tráfego:** use uma VPN no Mac junto com o `roaming on`. Não precisa de nada no celular.
- **O plano bloqueia hotspot:** aí não tem jeito. Confira no app da operadora ou do eSIM.
