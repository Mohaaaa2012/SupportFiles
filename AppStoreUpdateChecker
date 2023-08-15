//
//  AppStoreUpdateChecker.swift
//
//  Created by Mohamed Mostafa on 15/08/2023.
//

import Foundation

struct AppStoreUpdateChecker {

    static func insNewVersionAvailable(completion:@escaping(Bool)->()) {
        
        guard let bundleID = Bundle.main.bundleIdentifier,
              let currentVersionNumber = Bundle.main.releaseVersionNumber,
              let url = URL(string: "https://itunes.apple.com/lookup?bundleId=\(bundleID)") else {return}
        
        var request =  URLRequest(url:url)
        request.httpMethod = "GET"
        
        let task = URLSession.shared.dataTask(with: request) { Data, URLResponse, Error in
            if let Data = Data {
                do {
                    let appStoreResponse = try JSONDecoder().decode(AppStoreResponse?.self,from: Data)
                    guard let latestVersionNumber = appStoreResponse?.results?.first?.version else {return }
                  latestVersionNumber > currentVersionNumber ? completion(true) : completion(false)
                    
                }catch let error {
                    print(error)
                    completion(false)
                }
            }else{
                completion(false)
            }
        }
        task.resume()
    }
}
