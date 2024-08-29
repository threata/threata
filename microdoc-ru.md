### Создание нового кошелька
```python
from peer import API

api = API('http://127.0.0.1')

seed = api.Wallet.generate_seed()
wallet = api.Wallet(seed)
address = wallet.get_address()

print('Секретная фраза: ' + seed)
print('Адрес кошелька: ' + address)
```

### Вход в кошелек по секретной фразе
```python
from peer import API

SEED = 'crypta crypta durov macaron baget'

api = API('http://127.0.0.1')

wallet = api.Wallet(SEED) 
address = wallet.get_address()

print('Адрес кошелька: ' + address)
```

### Получить баланс кошелька
```python
from peer import API

api = API('http://127.0.0.1')
wallet = api.Wallet(...) # см создание и вход в кошелек
balance = api.get_balance(wallet.get_address())

print('Баланс: ' + str(balance))
```

### Перевод средств на другой кошелек
```python
import time
from peer import API

ADDRESS = 'адрес получателя'

api = API('http://127.0.0.1')
wallet = api.Wallet(...) # см создание и вход в кошелек

transaction = api.Transaction(
    amount=10,                      # Кол-во монет для перевода
    sender=wallet.get_address(),    # Адрес кошелька отправителя
    receiver=ADDRESS,               # Адрес кошелька получателя
    fee=0,                          # Кол-во монет которые уйдут майнеру
    nonce=round(time.time() * 1000) # Уникальное значение транзакции
)
transaction = wallet.sign(transaction) # Подписываем транзакцию кошельком

api.add_transaction(transaction) # Отправляем транзакцию на блокчейн
```
