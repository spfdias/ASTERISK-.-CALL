# ASTERISK
CAMPANHA DIAL .CALL ASTERISK

1 - Criar uma pasta chamada Promocao

2 - Criar uma chamada das variaveis  vim buscalista.sh

3 -  Adicionar o conteudo abaixo

#!/bin/bash
while read linha
        do
        CLIENTE_NUM=`echo $linha | cut -d: -f1`
echo 'Channel:SIP/984023000/'$CLIENTE_NUM'' >> /Promocao/Teste3_tt-monkeys.call
echo 'MaxRetries: 2' >> /Promocao/Teste3_tt-monkeys.call
echo 'RetryTime: 60' >> /Promocao/Teste3_tt-monkeys.call
echo 'WaitTime: 30' >> /Promocao/Teste3_tt-monkeys.call
echo 'Context: from-trunk' >> /Promocao/Teste3_tt-monkeys.call
echo 'Priority: 2' >> /Promocao/Teste3_tt-monkeys.call
echo 'Application: Playback' >> /Promocao/Teste3_tt-monkeys.call
echo 'Data: tt-monkeys' >> /Promocao/Teste3_tt-monkeys.call
echo 'Set: CDR(cnum)='$CLIENTE_NUM'' >> /Promocao/Teste3_tt-monkeys.call

        cp -Rf /Promocao/Teste3_tt-monkeys.call /var/spool/asterisk/outgoing/
        sleep 35
        echo "" > /Promocao/Teste3_tt-monkeys.call
        done < /Promocao/lista.txt
        

4 - Salvar o arquivo .sh e dar as permissoes necessarias chmod -R 777 buscalista.sh  e chmod +x buscalista.sh

5 - Criar um arquivo  vim lista.txt e adicionar os numeros que farão parte desta campanha. Detalhe a ligação será feita 1 por vez linha a linha de acordo a leitura do script.

6 - Crie um arquivo tambem .call , no meu exemplo criei um Teste3_tt-monkeys.call  e mudei as permissoes  chown -R asterisk.asterisk Teste3_tt-monkeys.call

7 - Para viabilizar, execute o arquivo .sh  bash -xv buscalista.sh . No meu exemplo eu utilizei o trunk SIP/984023000 para efetuar as ligações
