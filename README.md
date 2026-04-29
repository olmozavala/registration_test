# Semi-Automatic Non-Rigid Registration

This Dash app registers PC3 data from `img2.npy` into the pixel space of a selected MRI slice from `img1.nii.gz` using corresponding landmarks selected by the user.

If `img1.nii.gz` is not present, the app falls back to `img1.png` so the interface can still be tested. If `img2.npy` is not present, it falls back to `img2.png`, then to a placeholder image.

## Run

```bash
UV_PROJECT_ENVIRONMENT=/home/olmozavala/uv/envs/eoasweb uv run python app.py
```

Then open the local Dash URL shown in the terminal.

## Workflow

1. Select the desired MRI slice with the slice slider.
2. Rotate or horizontally flip either MRI or PC3 if its orientation needs adjustment.
3. Click matching landmarks in the same order on the selected MRI slice and PC3 image.
4. Use the undo buttons if a point is misplaced.
5. Select at least three matching point pairs.
6. Click **Run registration**.
7. Click **Save registered PC3 2D NIfTI** to write a spatially referenced `.nii.gz` file in `registered_outputs/`.

The MRI is displayed in grayscale. Scalar PC3 data is displayed with a blue-to-red palette, and the registered PC3 output uses that same palette.

The app computes a thin-plate-spline inverse mapping from the selected MRI-slice coordinates into PC3 coordinates, then resamples raw scalar PC3 so the registered output has the same height and width as the selected MRI slice. Saved NIfTI results use the MRI affine shifted to the selected slice location, so the 2D registered PC3 slice remains in MRI world coordinates.
