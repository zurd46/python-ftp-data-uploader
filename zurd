import ftplib
import logging
import time

logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

def create_ftp_client(host, username, password):
    """Erstellt einen FTP-Client, um Dateien zu übertragen."""
    ftp = ftplib.FTP(host)
    ftp.login(username, password)
    return ftp

def upload_file(ftp_client, local_path, remote_path):
    """Lädt eine Datei auf den FTP-Server hoch."""
    with open(local_path, 'rb') as file:
        try:
            ftp_client.storbinary(f'STOR {remote_path}', file)
            logging.info(f"Datei erfolgreich hochgeladen: {local_path} -> {remote_path}")
        except Exception as e:
            logging.error(f"Fehler beim Hochladen der Datei: {e}")
            raise

if __name__ == "__main__":
    host = "domain.com"
    username = "username"
    password = "password"
    local_path = "/path/to/file/"
    remote_path = "/path/to/file/"

    while True:
        ftp_client = None  # Initialize ftp_client to None before the try block
        try:
            ftp_client = create_ftp_client(host, username, password)
            upload_file(ftp_client, local_path, remote_path)
        except Exception as e:
            logging.error(f"Ein Fehler ist aufgetreten: {e}")
        finally:
            if ftp_client:  # Now ftp_client is guaranteed to be defined
                ftp_client.quit()
                logging.info("FTP-Verbindung geschlossen.")

        logging.info("Warte 30 Sekunden, bevor der nächste Upload-Versuch startet.")
        time.sleep(30)
