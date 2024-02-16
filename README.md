using System;
using System.Net.Http;
using System.Text.Json;
using System.Threading.Tasks;
using System.Text;

public class Program
{
    public static async Task Main(string[] args)
    {
        MainRequestDataField requestData = CreateRequestData();
        byte[] encryptedData = EncryptionHelper.EncryptRequestData(requestData);
        byte[] signature = SignatureHelper.SignData(encryptedData);
        HttpResponseMessage response = await ApiHelper.SendRequestToApi(encryptedData, signature);
        await ProcessResponse(response);
    }

    private static MainRequestDataField CreateRequestData()
    {
        return new MainRequestDataField
        {
            RequestedID = "123456",
            SourceSystemName = SourceSystemNameEnum.System1,
            APItoken = "your_api_token",
            Purpose = PurposeEnum.Purpose1,
            SessionKey = "session_key"
        };
    }

    private static async Task ProcessResponse(HttpResponseMessage response)
    {
        // Implement response processing logic here
        byte[] encryptedResponseData = await response.Content.ReadAsByteArrayAsync(); // Placeholder
    }
}
