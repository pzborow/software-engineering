# AMI — Amazon Machine Images

**Opis**
Gotowy "obraz instalacyjny" serwera: OS + Twoje apki + konfiguracja, zamrożone w jednym artefakcie. Nowa instancja EC2 z niego startuje w sekundy — zawsze identycznie.

**Kluczowe koncepty**
- **AMI** — obraz systemu (kernel + dysk + metadane); punkt startowy instancji EC2.
- **Snapshot** — zdjęcie dysku (EBS); z niego powstaje AMI.
- **Sharing** — AMI może być prywatny (Twoje konto), udostępniony innym kontom albo publiczny.

**Key points**
- Tworzony z działającej instancji albo od zera (np. Packerem).
- Gwarantuje **spójność**: dev/staging/prod działają na dokładnie tym samym obrazie.
- Można go **udostępniać między kontami AWS** (albo zrobić publicznym).

**Example (AWS CLI)**
```bash
# co mam?
aws ec2 describe-images --owners self \
  --query 'Images[:5].[ImageId,Name,State]'

# AMI z działającej instancji (snapshot dysku + metadane)
aws ec2 create-image --instance-id i-0abc123 --name my-app-v42
# -> {"ImageId": "ami-0def456", ...}

# z tego AMI nowa instancja — identyczna, w sekundy
aws ec2 run-instances --image-id ami-0def456 --instance-type t3.small
```

Sharing i sprzątanie:
```bash
# udostępnij drugiemu kontu / cofnij
aws ec2 modify-image-attribute --image-id ami-0def456 \
  --launch-permission "Add=[{\"UserId\":\"123456789012\"}]"
aws ec2 modify-image-attribute --image-id ami-0def456 \
  --launch-permission "Remove=[{\"UserId\":\"123456789012\"}]"

# AMI nie da się "usunąć" — deregistrujesz (snapshoty dysku zostają!)
aws ec2 deregister-image --image-id ami-0def456
aws ec2 delete-snapshot --snapshot-id vol-snap-0abc   # dopiero tu kasujesz dane
```

**Pełny flow** — jak przygotować AMI krok po kroku:
```bash
# 1. uruchom bazową instancję (czysty Amazon Linux)
aws ec2 run-instances --image-id ami-0base --instance-type t3.micro \
  --security-group-ids sg-0abc --key-name mykey
# -> i-0abc123

# 2. wejdź SSH-em i skonfiguruj jak chcesz (zainstaluj apki, ustaw config)
ssh -i mykey.pem ec2-user@<ip>
sudo dnf install -y python3 nginx
sudo systemctl enable nginx
echo "print('hello')" > /home/ec2-user/app.py
exit

# 3. utwórz AMI z tej instancji (snapshot dysku + metadane)
aws ec2 create-image --instance-id i-0abc123 --name my-app-v42
# -> {"ImageId": "ami-0def456", ...}

# 4. poczekaj, aż będzie available
aws ec2 wait image-available --image-id ami-0def456

# 5. z tego AMI nowa instancja — identyczna, w sekundy
aws ec2 run-instances --image-id ami-0def456 --instance-type t3.small \
  --security-group-ids sg-0abc --key-name mykey

# 6. zweryfikuj — nowa instancja ma już wszystko zainstalowane
ssh -i mykey.pem ec2-user@<new-ip>
python3 /home/ec2-user/app.py   # -> hello
systemctl status nginx          # -> active (enabled)

# 7. (opcjonalnie) udostępnij innemu kontu
aws ec2 modify-image-attribute --image-id ami-0def456 \
  --launch-permission "Add=[{\"UserId\":\"987654321098\"}]"
```
