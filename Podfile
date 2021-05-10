platform :ios, '14.0'

target 'LTOGlobalMachineOutliner' do
  pod 'Alamofire'
  pod 'RxSwift'
  pod 'RxCocoa'
  pod 'Kingfisher'
  pod 'lottie-ios'
  pod 'AFNetworking'
  pod 'Mantle'
  pod 'SDWebImage'
  pod 'SnapKit'
  pod 'GCDWebServer'
  pod 'SwiftyJSON'
end

post_install do |installer|
  installer.sandbox.target_support_files_root.glob('**/*.xcconfig').each do |xcconfig_file|
    config = Xcodeproj::Config.new(xcconfig_file)
    config.attributes['LLVM_LTO'] = 'YES'
    config.attributes['GCC_OPTIMIZATION_LEVEL'] = 's'
    config.attributes['COMPILER_INDEX_STORE_ENABLE'] =  'NO'
    config.attributes['OTHER_CFLAGS'] ||= '$(inherited)'
    config.attributes['ENABLE_BITCODE'] = 'NO'
    config.save_as(xcconfig_file)
  end
end
