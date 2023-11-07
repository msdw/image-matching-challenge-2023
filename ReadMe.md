# Overview of my solution
I used https://www.kaggle.com/code/eduardtrulls/imc-2023-submission-example (thanks @eduardtrulls for this reference to start)
I used Super Point, SuperGlue and Colmap
As in the starter notebook, I used EfficientNet B7 to filter the point pairs. This process generated a database which served as input for incremental mapping in Colmap.

## SuperPoint & SuperGlue
SuperPoint and SuperGlue are used with almost default parameters except keypoint_threshold is set to 0.001. I tune image size and finally I choose 1460.

## Fine tuning SuperPoint
Best works with  nms_radius = 3 and keypoint_threshold = 0.001, up to 1200 matching pairs. similarity threshold = 2.2, n_matches >= 150

## Incremental Mapper
Using COLMAP with simple radial (https://colmap.github.io/cameras.html)
I used COLMAP's incremental mapper for reconstruction with almost default parameters except min_model_size is set to 3.

## Execution Time
The execution time of the solution is about 8h
Increasing the number of pairs matching to be assessed does not hold within the 9 hour timeframe.

## Noticed:
The reconstruction with Colmap, non-deterministic, caused performance differences of up to 3 points, which could have caused the lottery in the final classification. I have read that some have modified Colmap to make it deterministic.

## The untested points, read here there which would have deserved that I devote time to it:
- image rotation which seemed to be the way to get the best result.
- the use of the exif to help in the orientation of the image
- MagSac filtering also seems to be a good addon to explore in the future.

## The things that I failed to make work:
- Ransac approach to filter points
- Kornia ( LoFTR, KeyNetAffNetHardNet, or DISK)
- using other camera models with Colmap (radial, opencv,simple_radial_fisheye)
- I try to replace tf_efficientnet_b7 by other model architecture without success
- TTA (I try to used differents sizes of image)

## LB Scores
- Public LB Score: 0.482
- Private LB Score: 0.524
The chosen solutions are the ones that perform best on both the public leaderboard and the private leaderboard.

