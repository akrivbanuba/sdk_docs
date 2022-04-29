# Minimal SDK

**Minimal SDK** can be used in case your app has strict size limits.

### How Regular SDK and Minimal SDK differ

|                     | Regular SDK                                                                  | Minimal SDK                                                                                                                                                                   |
| ------------------- | ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Face Search         | Adaptive and neural network face search algorithms including ARKit for iOS\* | Neural network and ARKit (iOS) face search algorithms supported\*                                                                                                             |
| Bundle size         | 30 Mb on average (depends on a platform)\*\*                                 | 12-13 Mb\*\*\*                                                                                                                                                                |
| Neural Networks     | Neural Networks included based on SDK license terms                          | Not included                                                                                                                                                                  |
| Performance         | See technical specification                                                  | Performance can be weak on low-end iOS devices due to Neural Networks Face search algorithm usage. Lower performance on any Android devices (in comparison with Regular SDK). |
| Supported platforms | See system requirements                                                      | All platforms except Web (due to low performance)                                                                                                                             |

\* Adaptive face search algorithms provide better performance and more quality user experience on a broad range of devices and platforms. Neural network face search algorithms enable quality user experience only on top devices.\
\*\* Bundle size depends on a platform used, but in average it is about 30 mb size with basic Face AR SDK features set (regular version).\
\*\*\* With stripped libraries for unused architectures and with disabled bitcode (iOS).

:::note How can I get Minimal SDK? Contact your sales manager or write us on [info@banuba.com](mailto:info@banuba.com) to get Face AR SDK minimal version. :::
