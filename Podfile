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
    config.attributes['COMPILER_INDEX_STORE_ENABLE'] = 'NO'
    config.attributes['ENABLE_BITCODE'] = 'NO'
    config.attributes['OTHER_SWIFT_FLAGS'] ||= '$(inherited)'
    config.attributes['OTHER_SWIFT_FLAGS'] << ' -Xfrontend -lto=llvm-full -Xfrontend -emit-bc'
    config.attributes['EXCLUDED_ARCHS'] = 'armv7'
    config.save_as(xcconfig_file)
  end

  installer.sandbox.target_support_files_root.glob('Pods-*/Pods-*.xcconfig').each do |xcconfig_file|
    config = Xcodeproj::Config.new(xcconfig_file)
    config.other_linker_flags[:simple] << "-Wl,-mllvm,--enable-machine-outliner=always,-mllvm,--machine-outliner-reruns=2"
    config.save_as(xcconfig_file)
  end
end
