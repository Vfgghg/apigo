using System;
using System.IO;
using System.Security.Cryptography;
using System.Text;

public static class EncryptionHelper
{
    // Encrypts the provided data using RSA encryption
    public static byte[] EncryptData(byte[] data, RSAParameters publicKey)
    {
        using (RSA rsa = RSA.Create())
        {
            rsa.ImportParameters(publicKey);
            return rsa.Encrypt(data, RSAEncryptionPadding.OaepSHA256);
        }
    }

    // Decrypts the provided data using RSA decryption
    public static byte[] DecryptData(byte[] encryptedData, RSAParameters privateKey)
    {
        using (RSA rsa = RSA.Create())
        {
            rsa.ImportParameters(privateKey);
            return rsa.Decrypt(encryptedData, RSAEncryptionPadding.OaepSHA256);
        }
    }
}
